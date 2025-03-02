# Password Grant

The Password Grant is for first party clients that are able to hold secrets (ie not Browser or Native Mobile Apps)

::: tip
The client_credentials grant should only be used by clients that can hold a secret
:::

### Flow

A complete refresh token request will include the following parameters:

- **grant_type** must be set to `password`
- **client_id** is the client identifier you received when you first created the application
- **client_secret** if the client is confidential (has a secret), this must be provided
- **username**
- **password**
- **scope** (optional) 

::: details View sample password grant request
<code-group>
<code-block title="Query String" active>
```http request
POST /token HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded

grant_type=password
&client_id=xxxxxxxxx
&client_secret=xxxxxxxxx
&username=xxxxxxxxx
&password=xxxxxxxxx
&scope="contacts.read contacts.write"
```
</code-block>

<code-block title="Basic Auth">
```http request
POST /token HTTP/1.1
Host: example.com
Authorization: Basic Y4NmE4MzFhZGFkNzU2YWRhN

grant_type=password
&username=xxxxxxxxx
&password=xxxxxxxxx
&scope="contacts.read contacts.write"
```
</code-block>
</code-group>
:::

The authorization server will respond with the following response

- **token_type** will always be `Bearer`
- **expires_in** is the time the token will live in seconds
- **access_token** is a JWT signed token and is used to authenticate into the resource server
- **refresh_token** is a JWT signed token and can be used in with the [refresh grant](#refresh-token-grant) 
- **scope** is a space delimited list of scopes the token has access to

::: details View sample password grant response
```http request
HTTP/1.1 200 OK
Content-Type: application/json; charset=UTF-8
Cache-Control: no-store
Pragma: no-cache

{
  token_type: 'Bearer',
  expires_in: 3600,
  access_token: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiI1MTJhYjlhNC1jNzg2LTQ4YTYtOGFkNi05NGM1M2E4ZGM2NTEiLCJleHAiOjE2MDE3NjcyOTksIm5iZiI6MTYwMTc2MzY5OSwiaWF0IjoxNjAxNzYzNjk5LCJqdGkiOiJuZXcgdG9rZW4iLCJjaWQiOiJ0ZXN0IGNsaWVudCIsInNjb3BlIjoiIn0.sX6SWc2Af8jn-izFnrLgNIcNuZz_tRLl2p7M3CzQwKg',
  refresh_token: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjbGllbnRfaWQiOiIzNTYxNWYyZi0xM2ZhLTQ3MzEtODNhMS05ZTM0NTU2YWIzOTAiLCJhY2Nlc3NfdG9rZW5faWQiOiJuZXcgdG9rZW4iLCJyZWZyZXNoX3Rva2VuX2lkIjoidGhpcy1pcy1teS1zdXBlci1zZWNyZXQtcmVmcmVzaC10b2tlbiIsInNjb3BlIjoiIiwidXNlcl9pZCI6IjUxMmFiOWE0LWM3ODYtNDhhNi04YWQ2LTk0YzUzYThkYzY1MSIsImV4cGlyZV90aW1lIjoxNjAxNzY3Mjk5LCJpYXQiOjE2MDE3NjM2OTh9.SSa7miIdk3bxyzg0f3M9jKBXWjPgD4QEw-AU3SYvBk0',
  scope: 'contacts.read contacts.write'
}
```
:::
