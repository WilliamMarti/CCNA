
CRUD (Create, Read, Update, Delete) operations performed buy REST APIs

**Create** - Create new variable and set their initial values

**Read** - Retrieve value of a variable

**Update** - Change value of a variable

**Delete** - Delete a variable

HTTP uses verbs(aka methods) that map to these CRUD operations

REST APIs typically use HTTP


| CRUD   | HTTP      |
| ------ | --------- |
| Create | Post      |
| Read   | Get       |
| Update | Put/Patch |
| Delete | Delete    |
HTTP Header will include a:
- HTTP verb
- URI (Uniform Resource Identifier)

https://text.example.com/blah/blah

https:// - scheme
text.example.com - authority
/blah/blah - path

Additional HTTP Headers can be sent to server
Ex: Accept Header
	informs server about the types of data that can be sent back to the client

`Accept: application/json`

REST APIs don't *have* to use http

##### HTTP Response

Servers response will include a status code indicating a success or failure

First Digit indicates the class of response 

- 1XX Information, request received, continuing process
- 2XX Successful.  Received, understood, and accepts
- 3XX Redirection.  Further action needs to be taken
- 4XX Client Error.  Bad syntax or cannot be fulfilled
- 5XX Server Error.  Server failed to fulfill an apparently valid request


102 - Processing

200 - OK, Succeeded
201 - Created, Succeeded and new resource created

301 - Redirection.  Moved Permanently

403 - Unauthorized
404 - Not Found

500 - Internal Server Error

##### Restful or REST-based API

6 Constraints or rules of RESTful architecture:
1. Uniform Interface
2. Client-Server
3. Stateless
4. Cacheable or non-cachable
5. Layer System
6. Code-on-Demand (optional)

**Stateless** - Each API exchange is a separate event, independant of all past exchanges between the client and the server

REST APIs *must* support caching of data storing data for future use

Not all resources have to be cacheable, but cacheable resources must be declared as cacheable

##### REST API Authentication

Process of validating the identity of a user or system to ensure legitimate access to resources

Types of auth are **methods** or **schemes**

##### Auth Types

**Basic Auth** - Send username and password in every request, encoded base64

**Bearer Authentication** - Users a token (bearer) token as an HTTP Header in each request to verify the clients identity

**API Key Auth** - Requires unique key, typically included as an HTTP Header, to authenticate API requests

**OAuth 2.0** - A secure framework that grants access via access tokens, commonly used for delegated access and third party authentication


##### Basic Auth

Start Line - 3 pieces of info:
1. HTTP Method
2. URL
3. HTTP Version

`POST /api/v1/acl/rules HTTP/2`

Headers:
- Host 
- Authorization
- Content-Type
- User-Agent

Body -> Data / Content

Credentials are encoded in Base64.
NOT encrypted
Base64 is encoding, not encryption
Always use HTTP(S) TLS

Username/Password is sent in the format "username:password" in Base64

Simple and easy to implement
Credentials are sent in every request, could be stolen

##### Bearer Authentication

Uses a token instead of a username/password

Client first obtains a token with an authorization server
	Can be done with Basic Auth

For each API call, the client includes the HTTP Authorized Header

Bear means anyone who posses the token can use it.
- If attacker steals the token, they can make API calls
- Tokens expire

More secure than Basic Auth
Tokens Expire

If token is stolen, attacker can access API
Tokens need to be refreshed, add complexity
Needs HTTPs

##### API Key Authentication

Static key issued by API Provider
API Key is static and doesn't expire
Can be added to URL or HTTP Header, or COokie.
	Can be exposed in logs

Easier to implement than bearer auth
Good for tracking API usage

Keys grant full access until revoked
API keys must be rotated

##### OAuth2.0

Secure authentication framework that is widely used in modern web apps.
Provide *delegation* , granting 3rd party apps limited access to resources on behalf of the resources owner.
No need to share the resources owners credentials with the 3rd party

Ex:
- Logging in with Google
- Connect apps to social media account
- Calendar integrating

4x Parties:
1. Resources Owner
2. Client App-account
3. Auth Server
4. Resource Server

Process:

1. **Client App** - Requests auth from resource owner(you) to access the resource (Google Cal)
2. **Resource Owner** - Grants auth by logging into their account and giving permissions
3. **Client App** - exchanges the authorization grant for an access token from the auth server
4. **Auth Server** - provides an access token to the resource server
5. **Client App** - send the access token to the resource server
6. Resource Server validates the access token and provides the requested resource(calendar data) to the client app

Access Token in #4 functions just like bearer tokens
- It grants access to the specified resources within the appropriate scope of access
- Access tokens (granted by Auth server) to obtain new access tokens without requiring the user to log in every time.  


 