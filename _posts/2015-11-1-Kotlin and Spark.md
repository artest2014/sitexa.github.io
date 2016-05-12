---
layout: post
title: Kotlin and Spark
category: 'java'
---

## 1.Kotlin

Kotlin is a new programming language from Jetbrains, the makers of some of the best programming tools in the business, including Intellij IDEA, an IDE for Java and other languages. As a leader in the Java community, Jetbrains understands the pains of Java and the many benefits of the JVM. Not wanting to throw the baby out with the bathwater, Jetbrains designed Kotlin to run on the JVM to get the best out of that platform.

They didn’t constrain it to this runtime, however — developers can also compile their Kotlin code into JavaScript, allowing it to be used in environments like Node.js. To work with untyped and typed environments like these, Kotlin is statically typed by default, but allows developers to define dynamic types as well. This balance provides great power and many opportunities.       

## 2.Why Kotlin?
        
Mike Hearn does a spectacular job explaining why you should consider using Kotlin. In his article, he lists the following reasons:

+   Kotlin compiles to JVM bytecode and JavaScript
+   Kotlin comes from industry, not academia
+   Kotlin is open source and costs nothing to adopt
+   Kotlin programs can use existing Java or JavaScript frameworks
+   The learning curve is very low
+   Kotlin doesn’t require any particular style of programming (OO or functional)
+   Kotlin can be used in Android development in addition to others where Java and JavaScript work
+   There is already excellent IDE support (Intellij and Eclipse)
+   Kotlin is highly suitable for enterprise Java shops
+   It has the strong commercial support of an established software company
        
## 3.the API’s entry point
        

    fun main(args: Array<String>) = api(composer = ContainerComposer())
    {
        route(
                path("/login", to = LoginController::class, renderWith = "login.vm"),
                path("/authorize", to = AuthorizeController::class, renderWith = "authorize.vm"),
                path("/token", to = TokenController::class))
    }

Run it:
    
<img src="/images/kotlin.png">
    
When this main method is executed, Spark will fire up a Web server, and you can immediately hit it like this:
    
    http://localhost:4567/login

We get in browser:
    
<image src="/images/kotlin2.png">
    
       
## 4.Functions and Constructors
       
To create our Domain Specific Language (DSL) for hosting APIs, we’re using several of Kotlin’s syntactic novelties and language features. Firstly:

+   Constructors: In Kotlin, you do not use the new keyword to instantiate objects; instead, you use the class name together with parenthesis, as if you were invoking the class as a function (a la Python). In the above snippet, a new ContainerComposer object is being created by invoking its default constructor.
+   Functions: Functions, which begin with the fun keyword, can be defined in a class or outside of one (like we did above). This syntax means that we can write Object Oriented (OO) code or not. This will give you more options and potentially remove lots of boilerplate classes.
+   Single expression functions: The fluent API allows us to wire up all our routes in a single expression. When a function consists of a single expression like this, we can drop the curly braces and specify the body of our function after an equals symbol.
+   Omitting the return type: When a function does not return a value (i.e., when it’s “void”), the return type is Unit. In Kotlin, you do not have to specify this; it’s implied.
       
       

### resources:

+   [https://kotlinlang.org](https://kotlinlang.org/)
+   [http://sparkjava.com](http://sparkjava.com)
+   http://nordicapis.com/building-apis-on-the-jvm-using-kotlin-and-spark-part-1/