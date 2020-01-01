### Load Balancers
* Hardware LB is expensive. Scaling may need capacity.
* Software LB is popular. Ex: HAProxy.
* LB Algorithms
    * Round Robin
    * Round Robin with weighted server
    * Least connections
    * Least response time
    * Source IP hash
    * URL hash

### Caching
* Cache can be done in every layer such as, OS, DB, application node, distributed, webserver, CDN, browser.
* Distributed cache uses consistant hashing.
* Cache invalidation approaches
    * Write-through cache - Update DB and cache at the same time. Writes will be slower.
    * Write around cache - Write data directly to storage and bypass the cache. Reads will be slower.
    * Write back cache: Only cache is updated and returned. The sync will happen asynchronously or periodically. Risk of data loss.
* Cache eviction policies
    * FIFO
    * LIFO
    * LRU - Doubly LinkedList with Map.
    * Most recently used.

### Sharding
* Joins and ACID compliance is complex with sharding.
#### Data sharding approaches
* Horizontal partitioning - Putting different rows into different shard baxed on some range. Ex: Alphabetical
* Vertical partitioning: Divide based on tables/features.
* Directory partitioning: Query directory server, which holds mapping between each tuple key to its DB.
#### Sharding Criteria
* Hash based
* List partitioning - Ex: APAC, US, etc
* Composite partitioning: Combining above two.

### Proxy Server
* Used for request filtering
* Merge multiple same requests
* Log requests
* Add and remove headers for sticky sessions
* Serve static resources
* Hide implementation details - IP etc

### Message Queue
* Messages are stored on the queue by producer until they are  processed by consumer.
* Best suited for async communication between microservices.

### SQL vs NoSQL
* SQL is suitable when the schema is fixed. ACID compliance and mostly vertically scalable.
* In NoSQL columns can be added on the fly and horizontally scalable.

### Consistent Hashing
* We make ranges and put servers in the ring. That way, if a new server is added or removed, only its neighbors data has to be updated.

### Kafka
* It is a distributed streaming platform that is used to publish and subscribe to stream of records.
* It is fast, uses IO efficiently by batching and compressing records.
* Kafka Components
    * Producer sends data/message
    * Consumer receives data. Consumer can subscribe to multiple topics.
    * Broker: Producer and consumer interact through kafka server.
    * Cluster: Kafka is a distributed system with many servers.
    * Topic: Identifier for a unique stream.
    * Partition: Break kafka topic into multiple partitions.
    * Offset: Sequence id given to message as they arrive in partition.
    * Topic name + Partition Number + Offset can locate exact message.
    * Consumer group share same workload.

### Cassandra
* Wide column store designed to handle large amounts of data.
* Its masterless with ring architecture.