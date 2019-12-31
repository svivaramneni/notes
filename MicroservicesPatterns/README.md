## Microservices Patterns By Chris Richardson

### Escaping monolithic hell
Challenges with monolith
* Deployment is slow. 
* The path from code commit to production is long and arduous.
* Scaling is difficult.
* Delivering a reliable monolith is challenging.
* Locked into increasingly obsolete technology stack.

### Microservices
Microservices is an architectural style that functionally decomposes an application into a set of services which are loosely coupled and independently deployable.
* A key characteristic of the microservice architecture is that services are loosely coupled and communicated only via APIs(different datastore)

### Decomposition Strategies

#### The '4+1' View Model of Software Architecture
* Logical View: What developers create
    * **Elements**: Classes and packages
     * **Relations**: The relationships between them.
* Implementation View: What is produced by the build system
    * **Elements**:  Modules, (JARfiles) and components(WAR files or executables)
     * **Relations**: Their dependencies
* Process View: Running components
    * **Elements**: Processes
     * **Relations**: Inter-process communication.
* Deployment View: Processes running on "machines".
    * **Elements**: Machines and processes
     * **Relations**: Networking

* You should strive to use libraries for functionality that's unlikely to change.
* Organize services around business capabilities, so that they are stable and resulting in a stable architecture.
 *  DDD defines separate domain model for each subdomain and calls scope of domain model is a "bounded context".
 * SRP and CCP OO principles could be used while decomposing a monolith.

 ### Interprocess communication in a microservice architecture
 #### Communication Patterns
 * Remote procedure invocation
    * Synchronous request/response-based communication mechanisms, such as HTTP-based REST or gRPC.
    * Asynchronous, message-based communication mechanisms such as AMQP or STOMP
    * Robustness principle : Be conservative in what you do, be liberal in what you accept from others. Services should provide default values fro missing request attributes. Similarly clients should ignore any extra response attributes.
    * We could version REST Api's with path(v1/,  v2) or use HTTP content negotiation mechanism and include version number in MIME type.
    ```
    GET /orders/xyz HTTP/1.1
    Accept: application/vnd.example.resource+json; version=1
    ```
    * Message formats: Text based(JSON, XML), Binary (Protocol Buffers, Avro)
 * Circuit breaker
    * An RPI proxy that immediately rejects invocations for a timeout period after the number of consecutive failures exceeds a specified threshold. 
    * Netflix Hystrix (https://github.com/Netflix/Hystrix) is an open source library that implements this pattern.
    * It’s essential that you design your services to handle partial failure
* Service Discovery
    * Service instances have dynamically assigned network locations. Moreover, the set of service instances changes dynamically because of autoscaling, failures, and upgrades. Consequently, your client code must use a service discovery.
    * Service registry is a database of network locations of application service instances.
    * Spring cloud automatically integrates with Eureka for service discovery.
    * Application level service discovery handles when services are deployed on multiple deployment platforms. Ex: if you have some services deployed on kubernetes and some on legacy environment. 
    * Application level service discovery has additional overhead in coming up with libraries, registry etc.
 * Client-side discovery
    * A service client retrieves the list of available service instances from the service registry and load balances across them
 * Self registration
    * Service instances are automatically registered with the service registry by a third party.
 * Server-side discovery
    * A client makes a request to a router, which is responsible for service discovery
    * Benefit of platform-provided service discovery is that all aspects of service discovery are entirely handled by the deployment platform. Neither the services nor the clients contain any service discovery code. Consequently, the service discovery mechanism is readily available to all services and clients regardless of which language or framework they’re written in.
 * Asynchronous messaging
    * A message consists of a header and body. Header is a collection of name-value pairs(metadata about message)
    * Message Types
        * **Command**: It specifies the operation to invoke and its parameters.
        * **Event**: Indicates something notable has occured in the sender. Often a domain event, which represents a state change of domain object. Ex: Order.
    * Point-to-point channel delivers message to exactly one customer that reading from teh channel.
    * Publish-subscribe channel delivers each message to all attached consumers.
    * Asynchronous request/response by including a reply channel and message identifier in the request message. The receiver processes the message and sends the reply to the specified reply channel.
    * Factors to consider while choosing message broker
        * Supported programming languages
        * Supported messaging standards: AMQP, STOMP
        * Messaging ordering: Does it preserver ordering of the messages
        * Delivery guarantees
        * Persistence to disk to handle crashes
        * Scalability
        * Latency
        * Does the broker support competing consumers.
    * JMS message brokers such as ActiveMQ have queues and topics
    * AMQP based message brokers such as RabbitMQ have exchanges and queues.
    * Apache Kafka has topics.
    * Ordering of the message is important. Apache Kafka uses consumer group to achieve this. The message broker assigns each shard to a single receiver. Ex: Each event for a particular order(shard-key:orderid) is published to the same shard, which is read by a single consumer instance.
    * For non idempotent duplicate messages, we should write a custom handler to track(ID through DB) and discard duplicates.
 * Transactional outbox
    * Publish an event or message as part of a database transaction by saving it in an OUTBOX in the database.
    * A sophisticated solution for MessageRelay is to tail the database transaction log(commit log).

### Managing transactions with sagas
 * Some modern databases like MongoDB, Cassandra or message brokers such as RabbitMQ or Kafka doesn't support distributed transactions.
 * Distributed transacations rely on synchronous IPC, which reduces availability.
 * Todays architects prefer systems thats available rather than consistent.

#### Saga pattern
* Maintain data consistency across services using a sequence of local transactions that are coordinated using asynchronous messaging.
* When a step of a saga fails because of business rule violation, the saga must explicitly undo the updates made by previous steps by executing compensating transactions.
* In choreography based sagas, there is no central coordinator. Instead saga participants subscribe to each others events and respond accordingly.
* Choreography works well for simple sagas.
* In Orchestration based sagas, orchestrators sole responsibility is to tell the saga participants what to do.
* Using a state machine model makes designing, implementing and testing sagas easier.

### Implementing Queries in Microservices
* API composition pattern consists of an API composer and two or more provider services. The API composer implements a query by querying the providers and combining the results.
* CQRS: Implement a query that needs data from several services by using events to maintain  a readonly view that replicates data from services.
* Case for CQRS
    * Using the API composition pattern to retrieve data scattered across multiple services results in expensive, inefficient in-memory joins.
    *  The service that owns the data stores the data in a form or in a database that doesn’t efficiently support the required query.
    * The need to separate concerns means that the service that owns the data isn’t the service that should implement the query operation.

### External API Patterns
* APIs could be consumed by webapplications, mobile or third party party integrations.
* Its not practical for a client to perform API composition over the internet. They are slow, no encapsulation, may not support all protocols.
* **API Gateway**: Implement a service thats a entry point into the microservice based application from external API clients.
    * API gateway acts like a facade and supports requests routing, authentication, monitoring, caching and rate limiting.
    * Client teams should own their API module and common API gateway should be fully automated.
* **Backend for Frontend**: Implement a separate API gateway for each client.
    * Clear isolation improves reliability. Also, these can be scaled independently.
    * Code duplication of common components.
* API gateway should fanout service calls in parallel. Whether to use blocking threads(Java8 CompletableFutures) or non blocking threads(NodeJS) is upto the teams.
* Examples of API gateway frameworks: Netflix Zuul, Spring Cloud Gateway.
* GraphQL provides graph based query language. Excellent foundation for deveopling API gateway.

### Authentication and authorization
* API gateway should authenticate and pass tokens to the services.

### Observability
* Health check API
* Log aggregation through centralized logging server with provides searching and alerting.
* Distributed tracing by assinging unique ID to each external request.
* Application metrics
* Audit logging to log user interactions.

### Chassis
Build services on a framework or collection of frameworks that handle cross-cutting concerns, such as exception tracking, logging, health checks, circuit breaker, service discovery, externalized configuration and distributed tracing.

### Service Mesh
Route all network traffic in and out of services through a network layer that implements various concerns, including circuit breakers, distributed tracing, service discovery, load balancing, rule based traffic routing.
Ex: Istio, Linkerd and Conduit.

### Strangler Application
Modernize application by incrementally developing new (strangler) application around the legacy application.
#### Strategies for refactoring a monolith to microservices
* Implement new features as services - If you find yourself in a hole, stop digging.
* Separate the presentation tier and backend
* Breakup the monolith by extracting functionality into services.


  

