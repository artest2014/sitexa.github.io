---
layout: post
title: Spark micro-framework
category: 'technology'
---

Spark - A micro framework for creating web applications in Java 8 with minimal effort

##start
    <dependency>
        <groupId>com.sparkjava</groupId>
        <artifactId>spark-core</artifactId>
        <version>2.3</version>
    </dependency>
    
    get("/hello",(req,res)->{"Hello,world"});

##stop server: 
    
    stop();

##Routes
-   1,verb(get,post,put,delete,head,trace,connect,options);
   parameters, splat parameters
-   2, path (/hello,/users/:name);
-   3, callback (request,response->{}

##Request
    request.attributes();             // the attributes list
    request.attribute("foo");         // value of foo attribute
    request.attribute("A", "V");      // sets value of attribute A to V
    request.body();                   // request body sent by the client
    request.bodyAsBytes();            // request body as bytes
    request.contentLength();          // length of request body
    request.contentType();            // content type of request.body
    request.contextPath();            // the context path, e.g. "/hello"
    request.cookies();                // request cookies sent by the client
    request.headers();                // the HTTP header list
    request.headers("BAR");           // value of BAR header
    request.host();                   // the host, e.g. "example.com"
    request.ip();                     // client IP address
    request.params("foo");            // value of foo path parameter
    request.params();                 // map with all parameters
    request.pathInfo();               // the path info
    request.port();                   // the server port
    request.protocol();               // the protocol, e.g. HTTP/1.1
    request.queryMap();               // the query map
    request.queryMap("foo");          // query map for a certain parameter
    request.queryParams();            // the query param list
    request.queryParams("FOO");       // value of FOO query param
    request.queryParamsValues("FOO")  // all values of FOO query param
    request.raw();                    // raw request handed in by Jetty
    request.requestMethod();          // The HTTP method (GET, ..etc)
    request.scheme();                 // "http"
    request.servletPath();            // the servlet path, e.g. /result.jsp
    request.session();                // session management
    request.splat();                  // splat (*) parameters
    request.uri();                    // the uri, e.g. "http://example.com/foo"
    request.url();                    // the url. e.g. "http://example.com/foo"
    request.userAgent();              // user agent

##Response
    response.body("hello");
    response.header("foo","bar");
    response.raw();
    response.redirect("/example");
    response.status(401);
    response.type("text/xml");

##QueryMaps;
    request.queryMap().get("user", "name").value();
    request.queryMap().get("user").get("name").value();
    request.queryMap("user").get("age").integerValue();
    request.queryMap("user").toMap();

##Cookie
    request.cookies();                              // get map of all request cookies
    request.cookie("foo");                          // access request cookie by name
    response.cookie("foo", "bar");                  // set cookie with a value
    response.cookie("foo", "bar", 3600);            // set cookie with a max-age
    response.cookie("foo", "bar", 3600, true);      // secure cookie
    response.removeCookie("foo");                   // remove cookie

##Session
    request.session(true)                            // create and return session
    request.session().attribute("user")              // Get session attribute 'user'
    request.session().attribute("user", "foo")       // Set session attribute 'user'
    request.session().removeAttribute("user")        // Remove session attribute 'user'
    request.session().attributes()                   // Get all session attributes
    request.session().id()                           // Get session id
    request.session().isNew()                        // Check if session is new
    request.session().raw()                          // Return servlet object

##Filter
    before((request, response) -> {
        boolean authenticated;
        // ... check if authenticated
        if (!authenticated) {
            halt(401, "You are not welcome here");
        }
    });
    after((request,response)->{
        response.header("foo","bar");
    });

##Redirect
    response.redirect("/bar",301);

##Exception Mapping
    get("/throwexception", (request, response) -> {
        throw new NotFoundException();
    });
    
    exception(NotFoundException.class, (e, request, response) -> {
        response.status(404);
        response.body("Resource not found");
    });

##Static Files
    staticFileLocation("/public"); // Static files
    externalStaticFileLocation("/var/www/public"); // Static files

##ResponseTransformer
    get("/hello", (request, response) -> new MyMessage("Hello World"), gson::toJson);

##Views and Templates

####Velocity
    <dependency>
        <groupId>com.sparkjava</groupId>
        <artifactId>spark-template-velocity</artifactId>
        <version>2.3</version>
    </dependency>

####Freemarker
    <dependency>
        <groupId>com.sparkjava</groupId>
        <artifactId>spark-template-freemarker</artifactId>
        <version>2.3</version>
    </dependency>

####Mustache
    <dependency>
        <groupId>com.sparkjava</groupId>
        <artifactId>spark-template-mustache</artifactId>
        <version>2.3</version>
    </dependency>

####Handlebars
    <dependency>
        <groupId>com.sparkjava</groupId>
        <artifactId>spark-template-handlebars</artifactId>
        <version>2.3</version>
    </dependency>

####Jade
    <dependency>
        <groupId>com.sparkjava</groupId>
        <artifactId>spark-template-jade</artifactId>
        <version>2.3</version>
    </dependency>

###Thymeleaf
    <dependency>
        <groupId>com.sparkjava</groupId>
        <artifactId>spark-template-thymeleaf</artifactId>
        <version>2.3</version>
    </dependency>

####Jetbrick
    <dependency>
        <groupId>com.sparkjava</groupId>
        <artifactId>spark-template-jetbrick</artifactId>
        <version>2.3</version>
    </dependency>

###Pebble
    <dependency>
        <groupId>com.sparkjava</groupId>
        <artifactId>spark-template-pebble</artifactId>
        <version>2.3</version>
    </dependency>

####Water
    <dependency>
        <groupId>com.sparkjava</groupId>
        <artifactId>spark-template-water</artifactId>
        <version>2.3</version>
    </dependency>

##Embedded Server

####port

    port(9090)

####secure 

    secure(keystoreFile, keystorePassword, truststoreFile, truststorePassword);

####threadpool

    threadPool(maxThreads, minThreads, timeOutMillis);

##WebSocket
    
    webSocket("/echo", EchoWebSocket.class);
    init(); // Needed if you don't define any HTTP routes after your WebSocket routes

    @WebSocket
    public class EchoWebSocket {

        // Store sessions if you want to, for example, broadcast a message to all users
        private static final Queue<Session> sessions = new ConcurrentLinkedQueue<>();
    
        @OnWebSocketConnect
        public void connected(Session session) {
            sessions.add(session);
        }
    
        @OnWebSocketClose
        public void closed(Session session, int statusCode, String reason) {
            sessions.remove(session);
        }
    
        @OnWebSocketMessage
        public void message(Session session, String message) throws IOException {
            System.out.println("Got: " + message);   // Print message
            session.getRemote().sendString(message); // and send it back
        }
    }

##Other Web Server
    
    <filter>
        <filter-name>SparkFilter</filter-name>
        <filter-class>spark.servlet.SparkFilter</filter-class>
        <init-param>
            <param-name>applicationClass</param-name>
            <param-value>com.company.YourApplication</param-value>
        </init-param>
    </filter>
    
    <filter-mapping>
        <filter-name>SparkFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

##GZIP

    get("/some-path", (request, response) -> {
        // code for your get
        response.header("Content-Encoding", "gzip");
    });
    after((request, response) -> {
        response.header("Content-Encoding", "gzip");
    });
    
