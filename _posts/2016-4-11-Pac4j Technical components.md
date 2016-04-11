---
layout: post
title: Pac4j Technical Components
category: 'technology'
---

pac4j is an easy and powerful Java security engine to authenticate users, get their profiles and manage authorizations in order to secure a Java web application. It provides a very comprehensive security model and implementation guidelines. It is based on Java 8 and available under the Apache 2 license.

It is currently available for most frameworks / tools and supports most authentication / authorization mechanisms.

![image](/images/Pac4j.png)


##pac4j-core:

This is the core module of the project with the core classes/interfaces:

-   the *Client* interface is the **main API of the project** as it defines the contract that all clients must follow: redirect(WebContext,boolean), getCredentials(WebContext) and getUserProfile(Credentials,WebContext). A client is an authentication mechanism, it is responsible for starting the authentication process (indirect / stateful: IndirectClient) and then getting the credentials and the user profile (UI use case) or directly (direct / stateless: DirectClient) getting and validating credentials and getting the user profile (web services use case). A hierarchy of clients exists: FacebookClient, CasClient...
-   the *Clients* class is used to gather all clients (on the same callback url for stateful / indirect clients)
-   the *Credentials* class is the base class for all credentials. A hierarchy of credentials exists: CasCredentials, Saml2Credentials, UsernamePasswordCredentials...
-   the *UserProfile* class is the base class for all user profiles (it is associated with attributes definition and converters). A hierarchy of user profiles exists: CommonProfile, OAuth20Profile, FacebookProfile... The CommonProfile class inherits from the UserProfile class and implements all the common getters that profiles must have (getFirstName(), getEmail()...)
-   *AttributesDefinition*: it's the attributes definition for a specific type of profile
-   the *ProfileManager* class manages the user profile using the web context: it gets/sets/removes the current user profile
-   the *WebContext* interface represents a web context which can be implemented in J2E or another environment: it represents the current HTTP request response and session, regardless of the framework. It internally relies on a SessionStore
-   the *AuthorizationGenerator* is an interface to implement to compute roles and permissions from a user profile
-   the *Authorizer* class is a generic interface to implement to manage authorizations given a user profile and a web context. It has several implementations: RequireAnyRoleAuthorizer, XFrameOptionsHeader...
-   *Config*: it's the application configuration composed of clients and authorizers. It can be used with a ConfigFactory, a ConfigBuilder and a ConfigSingleton depending on the framework capabilities
-   *AuthorizationChecker* and its default implementation: DefaultAuthorizationChecker are meant to check authorizations on a user profile and web context in pac4j implementations
-   *ClientFinder* and its default implementation: DefaultClientFinder are meant to retrieve the current client(s) in the pac4j implementations
-   *MatchingChecker* and its default implementation: DefaultMatchingChecker are meant to check if the current request matches (regarding Matcher) and must be enforced to security checks (it is used in some pac4j implementations).

##pac4j-oauth:

This module is dedicated to OAuth client support:

-   the FacebookClient, TwitterClient... classes are the clients for all the providers: Facebook, Twitter...
-   the OAuthCredentials class is the credentials for OAuth support
-   the FacebookProfile, TwitterProfile... classes are the associated profiles, returned by the clients.
This module is based on the pac4j-core module, the scribe-java library for OAuth protocol support, the Jackson library for JSON parsing and the commons-lang3 library.
