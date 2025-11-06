>*It’s always useful to know as much about the technology stack behind a web application in order to exploit it. One simple way to get information about an application is to look at the 404 not found page. If the site hasn’t created a custom 404 page, it can be used to fingerprint the framework / language being used by the site.*
>
>by [0xdf](https://0xdf.gitlab.io/cheatsheets/404)

Same principle, but now for API Signatures, heavily inspired by [kiterunner signatures](https://github.com/assetnote/kiterunner/tree/main/api-signatures). 

Expected use of cheatsheet:
1. You trigger an error from the API.
2. Copy the full response or only the part of it.
3. Search for response matches here.

Want to add more content or fix something? 
Create an issue or pull request in the GitHub repo [for this page](https://github.com/w0ltage/blog/blob/v4/content/Articles/Default%20API%20Signatures.md)

---
## .NET

#### ASP.NET

- GET /Help
	- `API Help Page</title>`
	- `My ASP.NET Application</p>`
	- `<td class="api-documentation">`

- GET /notexist
	- `<Message>No HTTP resource was found that matches the request URI`

---
#### Kestrel

- GET / or /api/v2.0/pinga

```
HTTP/1.1 404 Not Found
Content-Length: 0
Server: Kestrel
```

---
## JavaScript

#### Adonis

- GET / or /notexist
	- `Route not found GET /`

---
#### Express

- GET /
	- `<pre>Cannot GET /</pre>`
	
	- *header*
		- `X-Powered-By: Express`

---
#### Fastify

- GET /
	- `Route GET:/ not found`

- GET /notexist
	- `Route GET:/ not found`

---
#### Hapi & Sails

- GET /
	- `"ResourceNotFound"`


- GET /notexist
	- `"ResourceNotFound"`

---
#### Koa JS

- GET /notexist
	- `Not Found`

---
#### Loopback JS

- GET / or /notexist
	- `"name":"NotFoundError"`
	
	- *response*
		- `powered-by-loopback-sm.png`

---
#### Nest 

- GET /
	- `{"statusCode":404,"message":"Cannot GET /","error":"Not Found"}`

- GET /notexist
	- `{"statusCode":404,"message":"Cannot GET /thisshouldnotexist","error":"Not Found"}`

---
#### Total JS

- GET /
	- *header*
		- `X-Powered-By: Total.js`

---
## Python

#### Django

- GET /
	- `<p>The requested resource was not found on this server.</p>`
	- `<title>Page not found at /</title>`
	- `Authentication credentials were not provided.`

- GET /api-auth/login/?next=/
	- `<title>Django REST framework</title>`

---
#### FastAPI

- GET /
	- `"detail":"Not Found"`

- GET /notexist
	- `"detail":"Not Found"`

---
#### Flask

- GET /notexist
	- `The requested URL was not found on the server. If you entered the URL manually please check your spelling and try again.`

---
#### Tornado

- GET /
	- *header*
		- `Server: TornadoServer`

- GET /notexist
	- `<html><title>404: Not Found</title><body>404: Not Found</body></html>`

---
## Java

#### Dropwizard

- GET /notexist
	- `"message":"HTTP 404 Not Found"`

---

#### Jetty

- GET /
	- `Problem accessing /. Reason:`
	
	- *header*
		- `Server: Jetty`

- GET /notexist
	- `Problem accessing /notexist. Reason:`

---
#### Play Framework

- GET /
	- `For request 'GET /'`

- GET /notexist
	- `For request 'GET /notexist'`

---
#### Spark

- GET /
	- `<html><body><h2>404 Not found</h2></body></html>`

- GET /notexist
	- `<html><body><h2>404 Not found</h2></body></html>`

---
#### Spring Boot

- GET /
	- `"message":"No message available","path":"/"}`
	- `Whitelabel Error Page`

- GET /notexist
	- `No message available`

- GET /profile
	- `{"_links" : {`

---
#### Tomcat

- GET /
	- `<title>HTTP Status 404 – Not Found</title>`

- GET /notexist
	- `<title>HTTP Status 404 – Not Found</title>`

---
## Go

#### Beego

- GET /
	- *response*
		- `Powered by beego 2.0.0`

- GET /notexist
	- *response*
		- `Powered by beego 2.0.0`

---
#### Echo (Golang)

- GET /notexist
	- `{"message":"Not Found"}`

---
#### Golang HTTP Library

- GET /
	- `404 page not found`

---
## PHP

#### CakePHP

- GET /
	- `CakePHP: the rapid development php framework`
	- `The requested address <strong>'/'</strong>`

- GET /notexist
	- `The requested address <strong>'/notexist'</strong>`

---
#### CodeIgniter

- GET /
	- `CodeIgniter:`
	- `ci_csrf_token`

---
#### Laravel

- *cookie*
	- `laravel_session`

- GET /
	- `<h2 class="details-heading">Environment &amp; details:</h2>`
	- `Whoops, looks like something went wrong.`

- GET /notexist
	- `<title>Not Found</title>`
	- `<link href="https://fonts.googleapis.com/css?family=Nunito" rel="stylesheet">`

---
#### Phalcon

- GET /
	- `IndexController handler class cannot be loaded`

---
#### Symfony

- GET /
	- `No route found for "GET /"`

- GET /app_dev.php
	- `You are not allowed to access this file.`

- GET /notexist
	- `Oops! An Error Occurred`

- GET /api/aaa
	- `Oops! An Error Occurred`

---
#### Yii Framework

- GET /
	- *response*
		- `YII_CSRF_TOKEN`
		- `YII-BLOCK-`
		- `<a href="http://www.yiiframework.com/">Yii Framework</a>`
		- `Powered by <a href="http://www.yiiframework.com/" rel="external">Yii Framework</a>`

---
## Ruby

#### Rails

- *cookie*
	- `_session_id`

- GET /
	- `No route matches [GET]`
	
	- *headers*
		- `"Server": "mod_(?:rails|rack)"`
		- `"X-Powered-By": "mod_(?:rails|rack)"`
	
	- *response*
		- `"csrf-param": "^authenticity_token"`
		- `<meta name="csrf-param" content="authenticity_token" />`

---
#### Sinatra

- GET /
	- `/__sinatra__/404.png`
	
	- *headers*
		- `Server: WEBrick`

---
## Infrastructure

#### Kong

- GET /
	- `no API found with those values`
	- `no Route matched with those values`

---
#### Nginx

- GET /
	- `<center><h1>403 Forbidden</h1></center>`
	- `<center><h1>404 Not Found</h1></center>`

---
