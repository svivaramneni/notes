* OAuth 2.0 is a protocol that allows distinct parties to share information and resources in a secure and reliable manner.
    * Not backward compatible
    * OAuth 2.0 protocol is actually an authorization protocol and not an authentication protocol. 
* What is Authentication? Validating whether a person is actually who they say they are.
* What is Authorization? What actions are allowed to perform after authentication.
* Federated Identity? Login into one application(Facebook) and access others (Foursquare, Amazon, etc). Only one login credentials to remember.
* OAuth 2.0 supports the exchange of information through different grant types.
    * Authorization code grant - Server side flow - More secure - Long term access - Complex - Support refresh tokens.
    * Implicit grant - client side flow - Untrusted clients - Best practice is to provide readonly tokens. - less Complex - Short term access
    * Resource owner password credential grant - less popular
    * Client credential grant - less popular
    * Custom grant
* Bearer token is simply a type of access token. Bearer token holds all the information necessary in the token itself. Anyone can use that token.
* For untrusted client applications (browser based), we should use access tokens.
* The ability to refresh access token is only available for trusted clients.
* How often do we refresh our client secret? Best practise is to do every 6 months/release.
* Token contains 2 key properties. Scope and Duration of Access. Multiple scopes can be stacked in a single request with space delimiter. A typical readonly token duration is 30 mins.
* Token revocation. We don't support. But helpful in some scenarios. ex: writes.
* Each application registration process includes getting following.
    * Client ID -
    * Client Secret
    * Redirection endpoint
    * Authorization endpoint
    * Token endpoint
```
Get Request
GET /authorize? response_type=code/token& client_id=[CLIENT_ID]& redirect_uri=[REDIRECT_URI]& scope=[SCOPE]& state=[STATE] HTTP/1.1 
```
* OAuth specification doesn't mandate any particular authentication scheme for client authentication. Basic/Form body etc.
* In the final specification, client application identifies itself by passing in an authorization header using the basic auth protocol. [CLIENT_ID]:[CLIENT_SECRET]
* Different token types. Bearer, mac and custom.
* Refresh Token
```
POST /token HTTP/1.1 Host: server.example.com Authorization: Basic [ENCODED_CLIENT_CREDENTIALS] Content-Type: application/x-www-form-urlencoded grant_type=refresh_token&refresh_token=[REFRESH_TOKEN]
```
* Refresh token lifetime is usually much longer. Days to weeks.
* Not supported for implicit grant. Because refresh token has to be persisted somewhere.

* Security best practices
    * Use TLS
    * Request minimal scopes
    * Use implicit grant for ready only. Also limit token expiration time.
    * Don't expose client credentials (CLIENT_ID, CLIENT_SECRET) to users.
    * Use authorization code grant flow whereever possible. most secure.
    * Use refresh tokens
    * Rotate client credentials with every major release.

