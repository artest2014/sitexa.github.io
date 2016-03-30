---
layout: post
title: Design patterns implemented in Java
category: 'technology'
---

Design patterns are formalized best practices that the programmer can use to solve common problems when designing an application or system.

Design patterns can speed up the development process by providing tested, proven development paradigms.

Reusing design patterns helps to prevent subtle issues that can cause major problems, and it also improves code readability for coders and architects who are familiar with the patterns.

##Abstract Factory

Provide an interface for creating families of related or dependent objects without specifying their concrete classes.

![image](/images/abstract-factory_1.png)

Use the Abstract Factory pattern when

-	a system should be independent of how its products are created, composed and represented
-	a system should be configured with one of multiple families of products
-	a family of related product objects is designed to be used together, and you need to enforce this constraint
-	you want to provide a class library of products, and you want to reveal just their interfaces, not their implementations

##Adapter

Convert the interface of a class into another interface the clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.

![image](/images/adapter.png)

Use the Adapter pattern when

-	you want to use an existing class, and its interface does not match the one you need
-	you want to create a reusable class that cooperates with unrelated or unforeseen classes, that is, classes that don't necessarily have compatible interfaces
-	you need to use several existing subclasses, but it's impractical to adapt their interface by subclassing every one. An object adapter can adapt the interface of its parent class.

##Async Method Invocation

Asynchronous method invocation is pattern where the calling thread is not blocked while waiting results of tasks. The pattern provides parallel processing of multiple independent tasks and retrieving the results via callbacks or waiting until everything is done.

![image](/images/async-method-invocation.png)

Use async method invocation pattern when

-	you have multiple independent tasks that can run in parallel
-	you need to improve the performance of a group of sequential tasks
-	you have limited amount of processing capacity or long running tasks and the caller should not wait the tasks to be ready

##Bridge

Decouple an abstraction from its implementation so that the two can vary independently.

![image](/images/bridge.png)

Use the Bridge pattern when

-	you want to avoid a permanent binding between an abstraction and its implementation. This might be the case, for example, when the implementation must be selected or switched at run-time.
-	both the abstractions and their implementations should be extensible by subclassing. In this case, the Bridge pattern lets you combine the different abstractions and implementations and extend them independently
-	changes in the implementation of an abstraction should have no impact on clients; that is, their code should not have to be recompiled.
-	you have a proliferation of classes. Such a class hierarchy indicates the need for splitting an object into two parts. Rumbaugh uses the term "nested generalizations" to refer to such class hierarchies
-	you want to share an implementation among multiple objects (perhaps using reference counting), and this fact should be hidden from the client. A simple example is Coplien's String class, in which multiple objects can share the same string representation.

##Builder

Separate the construction of a complex object from its representation so that the same construction process can create different representations.

![image](/images/builder_1.png)

Use the Builder pattern when

-	the algorithm for creating a complex object should be independent of the parts that make up the object and how they're assembled
-	the construction process must allow different representations for the object that's constructed

##Business Delegate

The Business Delegate pattern adds an abstraction layer between presentation and business tiers. By using the pattern we gain loose coupling between the tiers and encapsulate knowledge about how to locate, connect to, and interact with the business objects that make up the application.

![image](/images/business-delegate.png)

Use the Business Delegate pattern when

-	you want loose coupling between presentation and business tiers
-	you want to orchestrate calls to multiple business services
-	you want to encapsulate service lookups and service calls

##Caching

To avoid expensive re-acquisition of resources by not releasing the resources immediately after their use. The resources retain their identity, are kept in some fast-access storage, and are re-used to avoid having to acquire them again.

![image](/images/caching.png)

Use the Caching pattern(s) when

-	Repetitious acquisition, initialization, and release of the same resource causes unnecessary performance overhead.

##Callback

Callback is a piece of executable code that is passed as an argument to other code, which is expected to call back (execute) the argument at some convenient time.

![image](/images/callback.png)

Use the Callback pattern when

-	when some arbitrary synchronous or asynchronous action must be performed after execution of some defined activity.

##Chain of responsibility

Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.

![image](/images/chain_1.png)

Use Chain of Responsibility when

-	more than one object may handle a request, and the handler isn't known a priori. The handler should be ascertained automatically
-	you want to issue a request to one of several objects without specifying the receiver explicitly
-	the set of objects that can handle a request should be specified dynamically

##Command

Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

![image](/images/command.png)

Use the Command pattern when you want to

-	parameterize objects by an action to perform. You can express such parameterization in a procedural language with a callback function, that is, a function that's registered somewhere to be called at a later point. Commands are an object-oriented replacement for callbacks.
-	specify, queue, and execute requests at different times. A Command object can have a lifetime independent of the original request. If the receiver of a request can be represented in an address space-independent way, then you can transfer a command object for the request to a different process and fulfill the request there
-	support undo. The Command's execute operation can store state for reversing its effects in the command itself. The Command interface must have an added Unexecute operation that reverses the effects of a previous call to execute. Executed commands are stored in a history list. Unlimited-level undo and redo is achieved by traversing this list backwards and forwards calling unexecute and execute, respectively
-	support logging changes so that they can be reapplied in case of a system crash. By augmenting the Command interface with load and store operations, you can keep a persistent log of changes. Recovering from a crash involves reloading logged commands from disk and re-executing them with the execute operation
-	structure a system around high-level operations build on primitive operations. Such a structure is common in information systems that support transactions. A transaction encapsulates a set of changes to data. The Command pattern offers a way to model transactions. Commands have a common interface, letting you invoke all transactions the same way. The pattern also makes it easy to extend the system with new transactions

##Composite

Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

![image](/images/composite_1.png)

Use the Composite pattern when

-	you want to represent part-whole hierarchies of objects
-	you want clients to be able to ignore the difference between compositions of objects and individual objects. Clients will treat all objects in the composite structure uniformly

##Data Access Object

Object provides an abstract interface to some type of database or other persistence mechanism.

![image](/images/dao.png)

Use the Data Access Object in any of the following situations

-	when you want to consolidate how the data layer is accessed
-	when you want to avoid writing multiple data retrieval/persistence layers


##Decorator

Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

![image](/images/decorator.png)

Use Decorator

-	to add responsibilities to individual objects dynamically and transparently, that is, without affecting other objects
-	for responsibilities that can be withdrawn
-	when extension by subclassing is impractical. Sometimes a large number of independent extensions are possible and would produce an explosion of subclasses to support every combination. Or a class definition may be hidden or otherwise unavailable for subclassing

##Delegation

It is a technique where an object expresses certain behavior to the outside but in reality delegates responsibility for implementing that behaviour to an associated object.

![image](/images/delegation.png)

Use the Delegate pattern in order to achieve the following

-	Reduce the coupling of methods to their class
-	Components that behave identically, but realize that this situation can change in the future.


##Dependency Injection

Dependency Injection is a software design pattern in which one or more dependencies (or services) are injected, or passed by reference, into a dependent object (or client) and are made part of the client's state. The pattern separates the creation of a client's dependencies from its own behavior, which allows program designs to be loosely coupled and to follow the inversion of control and single responsibility principles.

![image](/images/dependency-injection.png)

Use the Dependency Injection pattern when

-	when you need to remove knowledge of concrete implementation from object
-	to enable unit testing of classes in isolation using mock objects or stubs

##Double Checked Locking

Reduce the overhead of acquiring a lock by first testing the locking criterion (the "lock hint") without actually acquiring the lock. Only if the locking criterion check indicates that locking is required does the actual locking logic proceed.

![image](/images/double_checked_locking_1.png)

Use the Double Checked Locking pattern when

-	there is a concurrent access in object creation, e.g. singleton, where you want to create single instance of the same class and checking if it's null or not maybe not be enough when there are two or more threads that checks if instance is null or not.
-	there is a concurrent access on a method where method's behaviour changes according to the some constraints and these constraint change within this method.

##Double Dispatch

Double Dispatch pattern is a way to create maintainable dynamic behavior based on receiver and parameter types.

![image](/images/double-dispatch.png)

Use the Double Dispatch pattern when

-	the dynamic behavior is not defined only based on receiving object's type but also on the receiving method's parameter type.

##Event Aggregator

A system with lots of objects can lead to complexities when a client wants to subscribe to events. The client has to find and register for each object individually, if each object has multiple events then each event requires a separate subscription. An Event Aggregator acts as a single source of events for many objects. It registers for all the events of the many objects allowing clients to register with just the aggregator.

![image](/images/classes.png)

Use the Event Aggregator pattern when

-	Event Aggregator is a good choice when you have lots of objects that are potential event sources. Rather than have the observer deal with registering with them all, you can centralize the registration logic to the Event Aggregator. As well as simplifying registration, a Event Aggregator also simplifies the memory management issues in using observers.

##Execute Around

Execute Around idiom frees the user from certain actions that should always be executed before and after the business method. A good example of this is resource allocation and deallocation leaving the user to specify only what to do with the resource.

![image](/images/execute-around.png)

Use the Execute Around idiom when

-	you use an API that requires methods to be called in pairs such as open/close or allocate/deallocate.

#Facade

Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.

![image](/images/facade_1.png)

Use the Facade pattern when

-	you want to provide a simple interface to a complex subsystem. Subsystems often get more complex as they evolve. Most patterns, when applied, result in more and smaller classes. This makes the subsystem more reusable and easier to customize, but it also becomes harder to use for clients that don't need to customize it. A facade can provide a simple default view of the subsystem that is good enough for most clients. Only clients needing more customizability will need to look beyond the facade.
-	there are many dependencies between clients and the implementation classes of an abstraction. Introduce a facade to decouple the subsystem from clients and other subsystems, thereby promoting subsystem independence and portability.
-	you want to layer your subsystems. Use a facade to define an entry point to each subsystem level. If subsystems are dependent, the you can simplify the dependencies between them by making them communicate with each other solely through their facades

##Factory Kit

Define a factory of immutable content with separated builder and factory interfaces.

![image](/images/factory-kit.png)

Use the Factory Kit pattern when

-	a class can't anticipate the class of objects it must create
-	you just want a new instance of a custom builder instead of the global one
-	you explicitly want to define types of objects, that factory can build
-	you want a separated builder and creator interface

##Factory Method

Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

![image](/images/factory-method_1.png)

Use the Factory Method pattern when

-	a class can't anticipate the class of objects it must create
-	a class wants its subclasses to specify the objects it creates
-	classes delegate responsibility to one of several helper subclasses, and you want to localize the knowledge of which helper subclass is the delegate

##Feature Toggle

Used to switch code execution paths based on properties or groupings. Allowing new features to be released, tested and rolled out. Allowing switching back to the older feature quickly if needed. It should be noted that this pattern, can easily introduce code complexity. There is also cause for concern that the old feature that the toggle is eventually going to phase out is never removed, causing redundant code smells and increased maintainability.

![image](/images/feature-toggle.png)

Use the Feature Toogle pattern when

-	Giving different features to different users.
-	Rolling out a new feature incrementally.
-	Switching between development and production environments.

##Fluent Interface

A fluent interface provides an easy-readable, flowing interface, that often mimics a domain specific language. Using this pattern results in code that can be read nearly as human language.

![image](/images/fluentinterface.png)

A fluent interface can be implemented using any of

-	Method Chaining - calling a method returns some object on which further methods can be called.
-	Static Factory Methods and Imports
-	Named parameters - can be simulated in Java using static factory methods.

Use the Fluent Interface pattern when

-	you provide an API that would benefit from a DSL-like usage
-	you have objects that are difficult to configure or use

##Flux

Flux eschews MVC in favor of a unidirectional data flow. When a user interacts with a view, the view propagates an action through a central dispatcher, to the various stores that hold the application's data and business logic, which updates all of the views that are affected.

![image](/images/flux.png)

Use the Flux pattern when

-	you want to focus on creating explicit and understandable update paths for your application's data, which makes tracing changes during development simpler and makes bugs easier to track down and fix.

##Flyweight

Use sharing to support large numbers of fine-grained objects efficiently.

![image](/images/flyweight_1.png)


The Flyweight pattern's effectiveness depends heavily on how and where it's used. Apply the Flyweight pattern when all of the following are true

-	an application uses a large number of objects
-	storage costs are high because of the sheer quantity of objects
-	most object state can be made extrinsic
-	many groups of objects may be replaced by relatively few shared objects once extrinsic state is removed
-	the application doesn't depend on object identity. Since flyweight objects may be shared, identity tests will return true for conceptually distinct objects.

##Front Controller

Introduce a common handler for all requests for a web site. This way we can encapsulate common functionality such as security, internationalization, routing and logging in a single place.

![image](/images/front-controller.png)


Use the Front Controller pattern when

-	you want to encapsulate common request handling functionality in single place
-	you want to implements dynamic request handling i.e. change routing without modifying code
-	make web server configuration portable, you only need to register the handler web server specific way

##Half-Sync/Half-Async

The Half-Sync/Half-Async pattern decouples synchronous I/O from asynchronous I/O in a system to simplify concurrent programming effort without degrading execution efficiency.

![image](/images/half-sync-half-async.png)


Use Half-Sync/Half-Async pattern when

-	a system possesses following characteristics:
    -		the system must perform tasks in response to external events that occur asynchronously, like hardware interrupts in OS
    -		it is inefficient to dedicate separate thread of control to perform synchronous I/O for each external source of event
    -		the higher level tasks in the system can be simplified significantly if I/O is performed synchronously.
-	one or more tasks in a system must run in a single thread of control, while other tasks may benefit from multi-threading.

##Intercepting Filter

Provide pluggable filters to conduct necessary pre-processing and post-processing to requests from a client to a target

![image](/images/intercepting-filter.png)


Use the Intercepting Filter pattern when

-	a system uses pre-processing or post-processing requests
-	a system should do the authentication/ authorization/ logging or tracking of request and then pass the requests to corresponding handlers
-	you want a modular approach to configuring pre-processing and post-processing schemes

##Interpreter

Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language.

![image](/images/interpreter_1.png)


Use the Interpreter pattern when there is a language to interpret, and you can represent statements in the language as abstract syntax trees. The Interpreter pattern works best when

-	the grammar is simple. For complex grammars, the class hierarchy for the grammar becomes large and unmanageable. Tools such as parser generators are a better alternative in such cases. They can interpret expressions without building abstract syntax trees, which can save space and possibly time
-	efficiency is not a critical concern. The most efficient interpreters are usually not implemented by interpreting parse trees directly but by first translating them into another form. For example, regular expressions are often transformed into state machines. But even then, the translator can be implemented by the Interpreter pattern, so the pattern is still applicable

##Iterator

Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

![image](/images/iterator_1.png)


Use the Iterator pattern

-	to access an aggregate object's contents without exposing its internal representation
-	to support multiple traversals of aggregate objects
-	to provide a uniform interface for traversing different aggregate structures

##Layers

Layers is an architectural style where software responsibilities are divided among the different layers of the application.

![image](/images/layers.png)


Use the Layers architecture when

-	you want clearly divide software responsibilities into differents parts of the program
-	you want to prevent a change from propagating throughout the application
-	you want to make your application more maintainable and testable

##Lazy Loading

Lazy loading is a design pattern commonly used to defer initialization of an object until the point at which it is needed. It can contribute to efficiency in the program's operation if properly and appropriately used.

![image](/images/lazy-loading.png)


Use the Lazy Loading idiom when

-	eager loading is expensive or the object to be loaded might not be needed at all

##Mediator

Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.

![image](/images/mediator_1.png)


Use the Mediator pattern when

-	a set of objects communicate in well-defined but complex ways. The resulting interdependencies are unstructured and difficult to understand
-	reusing an object is difficult because it refers to and communicates with many other objects
-	a behavior that's distributed between several classes should be customizable without a lot of subclassing

##Memento

Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later.

![image](/images/memento.png)


Use the Memento pattern when

-	a snapshot of an object's state must be saved so that it can be restored to that state later, and
-	a direct interface to obtaining the state would expose implementation details and break the object's encapsulation

##Message Channel

When two applications communicate using a messaging system they do it by using logical addresses of the system, so called Message Channels.

![image](/images/message-channel.png)


Use the Message Channel pattern when

-	two or more applications need to communicate using a messaging system

##Model-View-Controller

Separate the user interface into three interconnected components: the model, the view and the controller. Let the model manage the data, the view display the data and the controller mediate updating the data and redrawing the display.

![image](/images/model-view-controller.png)


Use the Model-View-Controller pattern when

-	you want to clearly separate the domain data from its user interface representation

##Model-View-Presenter

Apply a "Separation of Concerns" principle in a way that allows developers to build and test user interfaces.

![image](/images/model-view-presenter_1.png)


Use the Model-View-Presenter in any of the following situations

-	when you want to improve the "Separation of Concerns" principle in presentation logic
-	when a user interface development and testing is necessary.

##Monad

Monad pattern based on monad from linear algebra represents the way of chaining operations together step by step. Binding functions can be described as passing one's output to another's input basing on the 'same type' contract. Formally, monad consists of a type constructor M and two operations: bind - that takes monadic object and a function from plain object to monadic value and returns monadic value return - that takes plain type object and returns this object wrapped in a monadic value.

![image](/images/monad.png)


Use the Monad in any of the following situations

-	when you want to chain operations easily
-	when you want to apply each function regardless of the result of any of them

##MonoState

Enforces a behaviour like sharing the same state amongst all instances.

![image](/images/monostate.png)


Use the Monostate pattern when

-   The same state must be shared across all instances of a class.
-   Typically this pattern might be used everywhere a Singleton might be used. Singleton usage however is not transparent, Monostate usage is.
-   Monostate has one major advantage over singleton. The subclasses might decorate the shared state as they wish and hence can provide dynamically different behaviour than the base class.

Typical Use Case

-   the logging class
-   managing a connection to a database
-   file manager

##Multiton

Ensure a class only has limited number of instances, and provide a global point of access to them.

![image](/images/multiton.png)


Use the Multiton pattern when

-   there must be specific number of instances of a class, and they must be accessible to clients from a well-known access point

##Mute Idiom

Provide a template to supress any exceptions that either are declared but cannot occur or should only be logged; while executing some business logic. The template removes the need to write repeated try-catch blocks.

![image](/images/mute-idiom.png)


Use this idiom when

-   an API declares some exception but can never throw that exception. Eg. ByteArrayOutputStream bulk write method.
-   you need to suppress some exception just by logging it, such as closing a resource.

##Naked Objects

The Naked Objects architectural pattern is well suited for rapid prototyping. Using the pattern, you only need to write the domain objects, everything else is autogenerated by the framework.

![image](/images/naked-objects.png)


Use the Naked Objects pattern when

-   you are prototyping and need fast development cycle
-   an autogenerated user interface is good enough
-   you want to automatically publish the domain as REST services

##Null Object

In most object-oriented languages, such as Java or C#, references may be null. These references need to be checked to ensure they are not null before invoking any methods, because methods typically cannot be invoked on null references. Instead of using a null reference to convey absence of an object (for instance, a non-existent customer), one uses an object which implements the expected interface, but whose method body is empty. The advantage of this approach over a working default implementation is that a Null Object is very predictable and has no side effects: it does nothing.

![image](/images/null-object.png)


Use the Null Object pattern when

-   you want to avoid explicit null checks and keep the algorithm elegant and easy to read.

##Object Pool

When objects are expensive to create and they are needed only for short periods of time it is advantageous to utilize the Object Pool pattern. The Object Pool provides a cache for instantiated objects tracking which ones are in use and which are available.

![image](/images/object-pool.png)


Use the Object Pool pattern when

-   the objects are expensive to create (allocation cost)
-   you need a large number of short-lived objects (memory fragmentation)

##Observer

Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

![image](/images/observer_1.png)


Use the Observer pattern in any of the following situations

-   when an abstraction has two aspects, one dependent on the other. Encapsulating these aspects in separate objects lets you vary and reuse them independently
-   when a change to one object requires changing others, and you don't know how many objects need to be changed
-   when an object should be able to notify other objects without making assumptions about who these objects are. In other words, you don't want these objects tightly coupled

##Poison Pill

Poison Pill is known predefined data item that allows to provide graceful shutdown for separate distributed consumption process.

![image](/images/poison-pill.png)


Use the Poison Pill idiom when

-   need to send signal from one thread/process to another to terminate

##Private Class Data

Private Class Data design pattern seeks to reduce exposure of attributes by limiting their visibility. It reduces the number of class attributes by encapsulating them in single Data object.

![image](/images/private-class-data.png)


Use the Private Class Data pattern when

-   you want to prevent write access to class data members

##Producer Consumer

Producer Consumer Design pattern is a classic concurrency pattern which reduces coupling between Producer and Consumer by separating Identification of work with Execution of Work.

![image](/images/producer-consumer.png)


Use the Producer Consumer idiom when

-   decouple system by separate work in two process produce and consume.
-   addresses the issue of different timing require to produce work or consuming work

##Property

Create hierarchy of objects and new objects using already existing objects as parents.

![image](/images/property.png)


Use the Property pattern when

-   when you like to have objects with dynamic set of fields and prototype inheritance

##Prototype

Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

![image](/images/prototype_1.png)

Use the Prototype pattern when a system should be independent of how its products are created, composed and represented; and

-   when the classes to instantiate are specified at run-time, for example, by dynamic loading; or
-   to avoid building a class hierarchy of factories that parallels the class hierarchy of products; or
-   when instances of a class can have one of only a few different combinations of state. It may be more convenient to install a corresponding number of prototypes and clone them rather than instantiating the class manually, each time with the appropriate state

##Proxy

Provide a surrogate or placeholder for another object to control access to it.

![image](/images/proxy_1.png)

Proxy is applicable whenever there is a need for a more versatile or sophisticated reference to an object than a simple pointer. Here are several common situations in which the Proxy pattern is applicable

-   a remote proxy provides a local representative for an object in a different address space.
-   a virtual proxy creates expensive objects on demand.
-   a protection proxy controls access to the original object. Protection proxies are useful when objects should have different access rights.


##Publish Subscribe

Broadcast messages from sender to all the interested receivers.

![image](/images/publish-subscribe.png)


Use the Publish Subscribe Channel pattern when

-   two or more applications need to communicate using a messaging system for broadcasts.


##Reactor

The Reactor design pattern handles service requests that are delivered concurrently to an application by one or more clients. The application can register specific handlers for processing which are called by reactor on specific events. Dispatching of event handlers is performed by an initiation dispatcher, which manages the registered event handlers. Demultiplexing of service requests is performed by a synchronous event demultiplexer.

![image](/images/reactor.png)


Use Reactor pattern when

-   a server application needs to handle concurrent service requests from multiple clients.
-   a server application needs to be available for receiving requests from new clients even when handling older client requests.
-   a server must maximize throughput, minimize latency and use CPU efficiently without blocking.

##Reader Writer Lock

Suppose we have a shared memory area with the basic constraints detailed above. It is possible to protect the shared data behind a mutual exclusion mutex, in which case no two threads can access the data at the same time. However, this solution is suboptimal, because it is possible that a reader R1 might have the lock, and then another reader R2 requests access. It would be foolish for R2 to wait until R1 was done before starting its own read operation; instead, R2 should start right away. This is the motivation for the Reader Writer Lock pattern.

![image](/images/reader-writer-lock.png)


Application need to increase the performance of resource synchronize for multiple thread, in particularly there are mixed read/write operations.

##Repository

Repository layer is added between the domain and data mapping layers to isolate domain objects from details of the database access code and to minimize scattering and duplication of query code. The Repository pattern is especially useful in systems where number of domain classes is large or heavy querying is utilized.

![image](/images/repository.png)


Use the Repository pattern when

-   the number of domain objects is large
-   you want to avoid duplication of query code
-   you want to keep the database querying code in single place
-   you have multiple data sources

##Resource Acquisition Is Initialization

Resource Acquisition Is Initialization pattern can be used to implement exception safe resource management.

![image](/images/resource-acquisition-is-initialization.png)


Use the Resource Acquisition Is Initialization pattern when

-   you have resources that must be closed in every condition

##Servant

Servant is used for providing some behavior to a group of classes. Instead of defining that behavior in each class - or when we cannot factor out this behavior in the common parent class - it is defined once in the Servant.

![image](/images/servant-pattern.png)


Use the Servant pattern when

-   when we want some objects to perform a common action and don't want to define this action as a method in every class.


##Service Layer

Service Layer is an abstraction over domain logic. Typically applications require multiple kinds of interfaces to the data they store and logic they implement: data loaders, user interfaces, integration gateways, and others. Despite their different purposes, these interfaces often need common interactions with the application to access and manipulate its data and invoke its business logic. The Service Layer fulfills this role.

![image](/images/service-layer.png)


Use the Service Layer pattern when

-   you want to encapsulate domain logic under API
-   you need to implement multiple interfaces with common logic and data

##Service Locator

Encapsulate the processes involved in obtaining a service with a strong abstraction layer.

![image](/images/service-locator.png)


The service locator pattern is applicable whenever we want to locate/fetch various services using JNDI which, typically, is a redundant and expensive lookup. The service Locator pattern addresses this expensive lookup by making use of caching techniques ie. for the very first time a particular service is requested, the service Locator looks up in JNDI, fetched the relevant service and then finally caches this service object. Now, further lookups of the same service via Service Locator is done in its cache which improves the performance of application to great extent.

Typical Use Case

-   when network hits are expensive and time consuming
-   lookups of services are done quite frequently
-   large number of services are being used

##Singleton

Ensure a class only has one instance, and provide a global point of access to it.

![image](/images/singleton_1.png)


Use the Singleton pattern when

t-  here must be exactly one instance of a class, and it must be accessible to clients from a well-known access point
-   when the sole instance should be extensible by subclassing, and clients should be able to use an extended instance without modifying their code

Typical Use Case

-   the logging class
-   managing a connection to a database
-   file manager

##Specification

Specification pattern separates the statement of how to match a candidate, from the candidate object that it is matched against. As well as its usefulness in selection, it is also valuable for validation and for building to order

![image](/images/specification.png)


Use the Specification pattern when

-   you need to select a subset of objects based on some criteria, and to refresh the selection at various times
-   you need to check that only suitable objects are used for a certain role (validation)

##State

Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.

![image](/images/state_1.png)


Use the State pattern in either of the following cases

-   an object's behavior depends on its state, and it must change its behavior at run-time depending on that state
-   operations have large, multipart conditional statements that depend on the object's state. This state is usually represented by one or more enumerated constants. Often, several operations will contain this same conditional structure. The State pattern puts each branch of the conditional in a separate class. This lets you treat the object's state as an object in its own right that can vary independently from other objects.

##Step Builder

An extension of the Builder pattern that fully guides the user through the creation of the object with no chances of confusion. The user experience will be much more improved by the fact that he will only see the next step methods available, NO build method until is the right time to build the object.

![image](/images/step-builder.png)


Use the Step Builder pattern when the algorithm for creating a complex object should be independent of the parts that make up the object and how they're assembled the construction process must allow different representations for the object that's constructed when in the process of constructing the order is important.

##Strategy

Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

![image](/images/strategy_1.png)


Use the Strategy pattern when

-   many related classes differ only in their behavior. Strategies provide a way to configure a class either one of many behaviors
-   you need different variants of an algorithm. for example, you might define algorithms reflecting different space/time trade-offs. Strategies can be used when these variants are implemented as a class hierarchy of algorithms
-   an algorithm uses data that clients shouldn't know about. Use the Strategy pattern to avoid exposing complex, algorithm-specific data structures
-   a class defines many behaviors, and these appear as multiple conditional statements in its operations. Instead of many conditionals, move related conditional branches into their own Strategy class

##Template method

Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.

![image](/images/template-method_1.png)


The Template Method pattern should be used

-   to implement the invariant parts of an algorithm once and leave it up to subclasses to implement the behavior that can vary
-   when common behavior among subclasses should be factored and localized in a common class to avoid code duplication. This is good example of "refactoring to generalize" as described by Opdyke and Johnson. You first identify the differences in the existing code and then separate the differences into new operations. Finally, you replace the differing code with a template method that calls one of these new operations
-   to control subclasses extensions. You can define a template method that calls "hook" operations at specific points, thereby permitting extensions only at those points

##Thread Pool

It is often the case that tasks to be executed are short-lived and the number of tasks is large. Creating a new thread for each task would make the system spend more time creating and destroying the threads than executing the actual tasks. Thread Pool solves this problem by reusing existing threads and eliminating the latency of creating new threads.

![image](/images/thread-pool.png)


Use the Thread Pool pattern when

-   you have a large number of short-lived tasks to be executed in parallel

##Tolerant Reader

Tolerant Reader is an integration pattern that helps creating robust communication systems. The idea is to be as tolerant as possible when reading data from another service. This way, when the communication schema changes, the readers must not break.

![image](/images/tolerant-reader.png)


Use the Tolerant Reader pattern when

-   the communication schema can evolve and change and yet the receiving side should not break

##Twin

Twin pattern is a design pattern which provides a standard solution to simulate multiple inheritance in java

![image](/images/twin.png)


Use the Twin idiom when

-   to simulate multiple inheritance in a language that does not support this feature.
-   to avoid certain problems of multiple inheritance such as name clashes.

##Value Object

Provide objects which follow value semantics rather than reference semantics. This means value objects' equality are not based on identity. Two value objects are equal when they have the same value, not necessarily being the same object.

![image](/images/value-object.png)


Use the Value Object when

-   you need to measure the objects' equality based on the objects' value

##Visitor

Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.

![image](/images/visitor_1.png)

Use the Visitor pattern when

-   an object structure contains many classes of objects with differing interfaces, and you want to perform operations on these objects that depend on their concrete classes
-   many distinct and unrelated operations need to be performed on objects in an object structure, and you want to avoid "polluting" their classes with these operations. Visitor lets you keep related operations together by defining them in one class. When the object structure is shared by many applications, use Visitor to put operations in just those applications that need them
-   the classes defining the object structure rarely change, but you often want to define new operations over the structure. Changing the object structure classes requires redefining the interface to all visitors, which is potentially costly. If the object structure classes change often, then it's probably better to define the operations in those classes

