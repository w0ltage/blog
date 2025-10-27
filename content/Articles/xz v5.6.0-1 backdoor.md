---
date: 2024-03-30
---
While Linux enthusiasts and related parties panic over the backdoor in xz, let's study the brilliance of this backdoor.

For those who are not aware — the library `liblzma`, part of the `xz` package, which allows compressing files into something with the `.xz` extension, was found to contain a backdoor that allows an attacker to quietly connect to your SSH server.

Moreover, the backdoor exists only in the `.tar` archives attached to releases 5.6.0 and 5.6.1, while on Github the source code archives are only for "testing" the library, in an *obfuscated* form.

`liblzma` is also sometimes a dependency of OpenSSH. 
Usually, this can happen when the distro patches OpenSSH to support `Systemd` notifications, causing `libsystemd` to depend on `liblzma`. Therefore, vanilla OpenSSH is not vulnerable to this backdoor ([source](https://t.me/hackthishit/83?comment=365))

Even more interestingly, the backdoor was discovered **not** by a security researcher, but by an ordinary programmer who got curious about "why CPU usage increases 10 times when connecting via SSH."

Now, let's break down how the backdoor gets onto the system and compromises it:

0. In the configuration file, the script `build-to-host.m4` is executed, which modifies the `Makefile` for building if a process called `sshd` is running on the host in `/usr/bin`.

1. It does so through "testing" with the archives `bad-3-corrupt_lzma2.xz` and `good-large-compressed.lzma` (which are not used for tests anywhere else).

2. These tests lead to the execution of code compressed in `bad-3-corrupt_lzma2.xz`, which in turn extracts the archive `good-large-compressed.lzma`.

3. The code inside `good-large-compressed.lzma` runs, causing the injection of `liblzma_la-crc64-fast.o` (the backdoor itself) into `$builddir/src/liblzma/Makefile`.

4. After building and successful installation, the backdoor intercepts execution by replacing ifunc resolvers for `crc32_resolve()` and `crc64_resolve()`, changing the code to call `_get_cpuid()`.

> `ifunc` — a `glibc` mechanism that allows implementing a function in different ways and selecting between implementations at runtime.

5. The backdoor then monitors dynamic linking of libraries into the process via an attached `audit hook`, waiting for the `RSA_public_decrypt@got.plt` library to load.

6. When it sees `RSA_public_decrypt@got.plt` being loaded, the backdoor replaces the library address with the address of attacker-controlled code.

Done! 
Now, when connecting over SSH, in the context before key authentication, the process executes code controlled by the attacker =)

Summarizing the backdoor in a picture:

![[xz-backdoor-nutshell.png]]

For advanced pwners, malware developers, and other interested parties, it is recommended to read the [original email describing the backdoor](https://openwall.com/lists/oss-security/2024/03/29/4) and the [description of the backdoor situation on GitHub](https://gist.github.com/thesamesam/223949d5a074ebc3dce9ee78baad9e27).
