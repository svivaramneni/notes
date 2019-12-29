### Step1: Requirements Clarifications
* Define end goals.
* Exactly which part of the subsystem are we designing for.
* UI/Backend?
* Analytics?

### Step2: System Interface Definition
* Define what specific APIs are expected from the system. This will help in validating assumptions.
```java
Ex: postTweet(String tweetData, UserContext context)
                   markTweetFavorite(String tweetID, UserContext context)
```
Context object could contain data, such as current_time, user_location, user_id etc.

### Step3: Back-of-the-envelope estimation
* Estimate scale of the system. This will help in deciding, scaling, partitioning, load balancing and caching. Ex: number of tweets, views, etc.
* How much storage is needed?
* What type of content? Ex: phots, tweets, videos
* Network bandwidth usage?

### Step4: Defining the data model
* Identify various entities of the system and how they interact with each other.
* Data Management? Ex: Storage, transportation, encryption, etc.
* Entity Ex: User – userID, name, email, DOB etc
* Tweet: tweetID, content, tweetLocation, numberOfLikes, timestamp, etc.
* UserFollows: userID1, userID2
* SQL vs NoSQL ?

### Step5: High-level Design
* Draw a block diagram with 5-6 boxes representing core components.
* Ex: Client, load balancer, application servers, DB, File Storage etc.
* How reads vs writes can be handled?

### Step6: Detailed Design
* Dig deeper into 2 or 3 components.
* Discuss different approaches, their pros vs cons and why we prefer one vs other. What tradeoffs are we making?
* How to partition the data?
* Hot users (who tweet a lot) vs passive users?
* What data is accessed frequently?
* How much and at which layer should we introduce cache?
* What components needs load balancing?

### Step7: Identify and resolve bottlenecks
* Discuss as many bottlenecks as possible.
* Discuss different approaches to mitigate them.
* Is there a single point of failure? If so, how to mitigate?
* If we lose few servers, what happens?
* How do we monitor performance of our service? Do we get critical alerts?
