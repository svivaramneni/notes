* Effective Design meets business need to the extent that it can distinguish itself from its competition by means of software.
* DDD is about modeling ubiquitous language in an explicitly bounded context.
* It is collaborative. Businesspeople and developers must work together daily throughout the project.
* Structure of code should be modeled along with the business domain.
* When you are getting started, bounded context could be problem space. As we get more clarity, it could transition into solution space.
* Bounded context is where model is implemented, so a separate artifact should be generated for each bounded context.
* Every entity in domain driven design should be associated with only one context.
* One team should work on one bounded context. i.e. source code, database, interfaces etc.
* In DDD, the majority of the communication between entities should be a choreographed/reactive model. i.e. publish-subscribe model.
* Bounded context: What is the core?
* A common mistake when using REST to design resources, is to directly reflect domain resources. Instead, there should be abstraction for client specific needs.
* Event Storming: It allows to design a system that models structure and flow of the activities within the business in a collaborative way.
o	Orange: An event is something that happens at the business level your customers (domain experts) care about.
o	Action: Blue - What do we want to have happen?
o	Questions – Red – Things we have to do.
