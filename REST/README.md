### REST Drivers
* Heterogeneous Interoperability
* Devices : phones, tablets, cars
* Cloud native applications

### What is REST?
It is a architectural style based on HTTP. Not a protocol or a design pattern.
### Statelessness
* Each request must contain all of the inforation necessary for the server to understand the request. 
* It should not rely on any stored context on the server.
#### Cacheability
* Requests and responses must include information about their cacheability.
#### Resources and representations
* Resources are the key abstraction of REST. 
* Resource is not an entity. It could be one or more entities.
`/children/youngest`
`/children/grace`
* Resource is a more generic conceept than a document. 
* Resource identifier can be valid before the resource exists and each resource has a unique identifier.
* Since resources can be abstract concepts, a resource itself is never directly manipulated or sent over the network. Instead server and client exchange representation of resources.
* The server can and should offer multiple representaions(JSON/XML) of the same resource. Clients tell the server which representation formats they understand.
#### Self-descriptive messages
* Messages include enough information to describe how their payload is to be processed. Ex: media type
* Each message completely identifies the resource it concerns.
#### Hypermedia as the engine of application state (HATEOAS)
* Restful servers and clients shouldn't rely on a hardcoded interface. Instead, server should send set of URIs representing possible state transitions with each response.
```json
HTTP/1.1 200 OK
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
}
```
### Richardson's Maturity Model
* Level 0 : POX - Plain Old XML
* Level 1: Resources
* Level 2: HTTP Verbs
* Level 3: Hypermedia

Only Level 3 in this model can actually be considered REST.

* Content type header could be used for versioning when resource itself doesn't change, but links inside the body/content changes.


### Design Considerations while choosing API strategy.
* Coupling
* Chattiness
* Client complexity
* Cognitive complexity
* Caching
* Discoverability
* Versioning

### REST vs RPC vs GraphQL
* RPC is calling a function over remote call. It fits well for API's which are command, action oriented. Ex: Slack.
* For internal communication between microservices, gRPC maybe a good fit. Because its fast with less network overhead. Ex: Netflix, Google.
* RPC doesn't have good abstractions. Its easy to leak implementation details to the client. No discoverability, also function explosion.

* REST provides loose coupling. Also, provides discoverability with HATEOAS. Ex: Json-Api
* REST could be chatty with large payloads.

* With GraphQL you could specify exactly what property you need. Its almost like sending a query.
* Low network overhead. Typed schema. Fits to graph-like data well.
* Complex, Caching, Versioning is tricky.


| Type | Coupling        | Chattiness           | Client Complexity  | Cognitive complexity        | Caching           | Discoverability  | Versioning |
|:-------------|:-------------:|:-------------:|:------:|:-------------:|:-------------:|:------:|:-------------:|
|RPC  Functions   | High     | Medium | Low | Low  | Custom |  Bad   | Hard |
|REST Resources | low        | high       | Low | Low  | HTTP    | Good | Easy |
|GraphQL Queries| Medium| Low       | High | High | Custom | Good | ???   |


### REST vs OData


### OpenAPI


### JSON API







