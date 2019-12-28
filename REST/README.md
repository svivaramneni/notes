### REST Drivers
* Heterogeneous Interoperability
* Devices : phones, tablets, cars
* Cloud native applications

### What is REST?
It is a architectural style. Not a protocol or a design pattern.
### Statelessness
* Each request must contain all of the inforation necessary for the server to understand the request. 
* It should not rely on any stored context on the server.
#### Cacheability
* Requests and responses must include information about their cacheability.
#### Resources and representations
* Resources are the key abstraction of REST. 
* They are more generic conceept than a document. 
* Resource identifier can be valid before the resource exists and each resource has a unique identifier.
* Since resources can be abstract concepts, a resource itself is never directly manipulated or sent over the network. Instead server and client exchange representation of resources.
* The server can and should offer multiple representaions(JSON/XML) of the same resource. Clients tell the server which representation formats they understand.
#### Self-descriptive messages
* Messages include enough information to describe how their payload is to be processed. Ex: media type
* Each message completely identifies the resource it concerns.
#### Hypermedia as the engine of application state (HATEOAS)
* Restful servers and clients shouldn't rely on a hardcoded interface. Instead, server should send set of URIs representing possible state transitions with each response.
`HTTP/1.1 200 OK
Content-Type: application/vnd.acme.account+json
Content-Length: ...

{
    "account": {
        "account_number": 12345,
        "balance": {
            "currency": "usd",
            "value": 100.00
        },
        "links": {
            "deposit": "/accounts/12345/deposit",
            "withdraw": "/accounts/12345/withdraw",
            "transfer": "/accounts/12345/transfer",
            "close": "/accounts/12345/close"
        }
    }
}`


