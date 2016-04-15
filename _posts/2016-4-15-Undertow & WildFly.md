---
layout: post
title: Undertow & WildFly
category: 'technology'
---

##Undertow

Undertow is a web server designed to be used for both blocking and non-blocking tasks. Some of its main features are:

-   High Performance
-   Embeddable
-   Servlet 3.1
-   Web Sockets
-   Reverse Proxy

There and two main ways that Undertow can be used, either by directly embedding it in your code, or as part of the Wildfly Application Server. This guide mostly focuses on the embedded API’s, although a lot of the content is still relevant if you are using Wildfly, it is just that the relevant functionality will generally be exposed via XML configuration rather than programatic configuration.

    public class HelloWorldServer {
        public static void main(final String[] args) {
            Undertow server = Undertow.builder()
                    .addHttpListener(8080, "localhost")
                    .setHandler(new HttpHandler() {
                        public void handleRequest(final HttpServerExchange exchange) throws Exception {
                            exchange.getResponseHeaders().put(Headers.CONTENT_TYPE, "text/plain");
                            exchange.getResponseSender().send("Hello World");
                        }
                    }).build();
            server.start();
        }
    }
    

##WildFly

WildFly is a flexible, lightweight, managed application runtime that helps you build amazing applications.

(formerly known as JBoss Application Server)


Key Features
------------
* Java EE 7 support
* Fast Startup
* Small Footprint
* Modular Design
* Unified Configuration and Management
* Distributed Domain Management
* OSGi

Release Notes
-------------
You can obtain the 10.0.0.Beta1 release notes here:

https://issues.jboss.org/secure/ReleaseNote.jspa?projectId=12313721&version=12327160

Getting Started
---------------
WildFly requires JDK 1.8 or later. For information regarding installation
of the JDK, see http://www.oracle.com/technetwork/java/index.html

WildFly has two modes of operation: Standalone and Domain. For more
information regarding these modes, please refer to the documentation 
available on the JBoss.org site:

https://docs.jboss.org/author/display/WFLY10/Documentation


Starting a Standalone Server
----------------------------
A WildFly standalone server runs a single instance.

<JBOSS_HOME>/bin/standalone.sh      (Unix / Linux)

<JBOSS_HOME>\bin\standalone.bat     (Windows)


Starting a Managed Domain
-------------------------
A WildFly managed domain allows you to control and configure multiple instances,
potentially across several physical (or virtual) machines. The default 
configuration includes a domain controller and a single server group with three 
servers (two of which start automatically), all running on the localhost.

<JBOSS_HOME>/bin/domain.sh      (Unix / Linux)

<JBOSS_HOME>\bin\domain.bat     (Windows)
 

Accessing the Web Console
-------------------------
Once the server has started you can access the landing page:

http://localhost:8080/

This page includes links to online documentation, quick start guides, forums 
and the administration console.


Stopping the Server
-------------------
A WildFly server can be stopped by pressing Ctrl-C on the command line.
If the server is running in a background process, the server can be stopped
using the JBoss CLI:

<JBOSS_HOME>/bin/jboss-cli.sh --connect --command=:shutdown      (Unix / Linux)

<JBOSS_HOME>\bin\jboss-cli.bat --connect --command=:shutdown     (Windows)