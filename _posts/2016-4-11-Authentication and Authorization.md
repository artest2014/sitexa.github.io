---
layout: post
title: Authentication and Authorization
category: 'technology'
---

Authentication is any process by which you verify that someone is who they claim they are. 
Authorization is any process by which someone is allowed to be where they want to go, 
or to have information that they want to have.

-   Authentication type：
    -   basic
    -   digest
-   Authentication provider：
    -   anonymous
    -   dbd
    -   dbm
    -   file
    -   ldap
    -   socache
-   Authorization：
    -   ldap
    -   dbd
    -   dbm
    -   groupfile
    -   host
    -   owner
    -   user
    
##Apache HttpClient

HttpClient supports three different types of http authentication schemes: Basic, Digest and NTLM. These can be used to authenticate with http servers or proxies.

-   Server Authentication
    HttpClient handles authenticating with servers almost transparently, the only thing a developer must do is actually provide the login credentials. These credentials are stored in the HttpState instance and can be set or retrieved using the setCredentials(AuthScope authscope, Credentials cred) and getCredentials(AuthScope authscope) methods.
    The automatic authorization built in to HttpClient can be disabled with the method setDoAuthentication(boolean doAuthentication) in the HttpMethod class. The change only affects that method instance.
-   Preemptive Authentication
    Preemptive authentication can be enabled within HttpClient. In this mode HttpClient will send the basic authentication response even before the server gives an unauthorized response in certain situations, thus reducing the overhead of making the connection. To enable this use the following:
    
    client.getParams().setAuthenticationPreemptive(true);
    
    Preemptive authentication mode also requires default Credentials to be set for the target or proxy host against which preemptive authentication is to be attempted. Failure to provide default credentials will render the preemptive authentication mode ineffective.
    
    Credentials defaultcreds = new UsernamePasswordCredentials("username", "password");
    client.getState().setCredentials(new AuthScope("myhost", 80, AuthScope.ANY_REALM), defaultcreds);
    
-   Security aspects of server authentication
    
    Use default credentials with caution when developing applications that may need to communicate with untrusted web sites or web applications. When preemptive authentication is activated or credentials are not explicitly given for a specific authentication realm and host HttpClient will use default credentials to try to authenticate with the target site. If you want to avoid sending sensitive credentials to an untrusted site, narrow the credentials scope as much as possible: always specify the host and, when known, the realm the credentials are intended for.
    Setting credentials with AuthScope.ANY authentication scope (null value for host and/or realm) is highly discouraged in production applications. Doing this will result in the credentials being sent for all authentication attempts (all requests in the case of preemptive authentication). Use of this setting should be limited to debugging only.
    
    // To be avoided unless in debug mode
    Credentials defaultcreds = new UsernamePasswordCredentials("username", "password");
    client.getState().setCredentials(AuthScope.ANY, defaultcreds);
    
-   Proxy Authentication
    
-   Authentication Schemes
    
    The following authentication schemes are supported by HttpClient.
    
    -   Basic - Basic authentication is the original and most compatible authentication scheme for HTTP. Unfortunately, it is also the least secure as it sends the username and password unencrypted to the server. Basic authentication requires an instance of UsernamePasswordCredentials (which NTCredentials extends) to be available, either for the specific realm specified by the server or as the default credentials.
    -   Digest - Digest authentication was added in the HTTP 1.1 protocol and while not being as widely supported as Basic authentication there is a great deal of support for it. Digest authentication is significantly more secure than basic authentication as it never transfers the actual password across the network, but instead uses it to encrypt a "nonce" value sent from the server.
                 Digest authentication requires an instance of UsernamePasswordCredentials (which NTCredentials extends) to be available either for the specific realm specified by the server or as the default credentials.
    -   NTLM - NTLM is the most complex of the authentication protocols supported by HttpClient. It is a proprietary protocol designed by Microsoft with no publicly available specification. Early version of NTLM were less secure than Digest authentication due to faults in the design, however these were fixed in a service pack for Windows NT 4 and the protocol is now considered more secure than Digest authentication.


##Example

-    BasicAuthenticationExample.java


        import org.apache.commons.httpclient.HttpClient;
        import org.apache.commons.httpclient.UsernamePasswordCredentials;
        import org.apache.commons.httpclient.auth.AuthScope;
        import org.apache.commons.httpclient.methods.GetMethod;
            
        /**
         * A simple example that uses HttpClient to perform a GET using Basic
         * Authentication. Can be run standalone without parameters.
         *
         * You need to have JSSE on your classpath for JDK prior to 1.4
         *
         * @author Michael Becke
         */
        public class BasicAuthenticationExample {
        
        /**
         * Constructor for BasicAuthenticatonExample.
         */
        public BasicAuthenticationExample() {
            super();
        }
    
        public static void main(String[] args) throws Exception {
            HttpClient client = new HttpClient();
    
            // pass our credentials to HttpClient, they will only be used for
            // authenticating to servers with realm "realm" on the host
            // "www.verisign.com", to authenticate against
            // an arbitrary realm or host change the appropriate argument to null.
            client.getState().setCredentials(
                new AuthScope("www.verisign.com", 443, "realm"),
                new UsernamePasswordCredentials("username", "password")
            );
    
            // create a GET method that reads a file over HTTPS, we're assuming
            // that this file requires basic authentication using the realm above.
            GetMethod get = new GetMethod("https://www.verisign.com/products/index.html");
    
            // Tell the GET method to automatically handle authentication. The
            // method will use any appropriate credentials to handle basic
            // authentication requests.  Setting this value to false will cause
            // any request for authentication to return with a status of 401.
            // It will then be up to the client to handle the authentication.
            get.setDoAuthentication( true );
    
            try {
                // execute the GET
                int status = client.executeMethod( get );
    
                // print the status and response
                System.out.println(status + "\n" + get.getResponseBodyAsString());
    
            } finally {
                // release any connection resources used by the method
                get.releaseConnection();
            }
        }
        }
    
    
-   CustomAuthenticationExample.java
    
        import java.util.ArrayList;
    	import java.util.Collection;
    	
    	import org.apache.commons.httpclient.Credentials;
    	import org.apache.commons.httpclient.HttpMethod;
    	import org.apache.commons.httpclient.auth.AuthPolicy;
    	import org.apache.commons.httpclient.auth.AuthScheme;
    	import org.apache.commons.httpclient.auth.AuthenticationException;
    	import org.apache.commons.httpclient.auth.MalformedChallengeException;
    	import org.apache.commons.httpclient.params.DefaultHttpParams;
    	import org.apache.commons.httpclient.params.HttpParams;
    	
    	/**
    	 * A simple custom AuthScheme example.  The included auth scheme is meant 
    	 * for demonstration purposes only.  It does not actually implement a usable
    	 * authentication method.
    	 */
    	public class CustomAuthenticationExample {
    	
    	    public static void main(String[] args) {
    	        
    	        // register the auth scheme
    	        AuthPolicy.registerAuthScheme(SecretAuthScheme.NAME, SecretAuthScheme.class);
    	
    	        // include the scheme in the AuthPolicy.AUTH_SCHEME_PRIORITY preference,
    	        // this can be done on a per-client or per-method basis but we'll do it
    	        // globally for this example
    	        HttpParams params = DefaultHttpParams.getDefaultParams();        
    	        ArrayList schemes = new ArrayList();
    	        schemes.add(SecretAuthScheme.NAME);
    	        schemes.addAll((Collection) params.getParameter(AuthPolicy.AUTH_SCHEME_PRIORITY));
    	        params.setParameter(AuthPolicy.AUTH_SCHEME_PRIORITY, schemes);
    	        
    	        // now that our scheme has been registered we can execute methods against
    	        // servers that require "Secret" authentication... 
    	    }
    	    
    	    /**
    	     * A custom auth scheme that just uses "Open Sesame" as the authentication
    	     * string.
    	     */
    	    private class SecretAuthScheme implements AuthScheme {
    	
    	        public static final String NAME = "Secret";
    	
    	        public SecretAuthScheme() {
    	            // All auth schemes must have a no arg constructor.
    	        }
    	        public String authenticate(Credentials credentials, HttpMethod method)
    	            throws AuthenticationException {
    	            return "Open Sesame";
    	        }
    	        public String authenticate(Credentials credentials, String method,
    	                String uri) throws AuthenticationException {
    	            return "Open Sesame";
    	        }
    	        public String getID() {
    	            return NAME;
    	        }
    	        public String getParameter(String name) {
    	            // this scheme does not use parameters, see RFC2617Scheme for an example
    	            return null;
    	        }
    	        public String getRealm() {
    	            // this scheme does not use realms
    	            return null;
    	        }
    	        public String getSchemeName() {
    	            return NAME;
    	        }
    	        public boolean isConnectionBased() {
    	            return false;
    	        }
    	        public void processChallenge(String challenge)
    	                throws MalformedChallengeException {
    	            // Nothing to do here, this is not a challenge based
    	            // auth scheme.  See NTLMScheme for a good example.
    	        }
    	        public boolean isComplete() {
    	            // again we're not a challenge based scheme so this is always true
    	            return true;
    	        }
    	    }
    	}


-   InteractiveAuthenticationExample.java

    
        import java.io.BufferedReader;
        import java.io.IOException;
        import java.io.InputStreamReader;
        import org.apache.commons.httpclient.Credentials;
        import org.apache.commons.httpclient.HttpClient;
        import org.apache.commons.httpclient.NTCredentials;
        import org.apache.commons.httpclient.UsernamePasswordCredentials;
        import org.apache.commons.httpclient.auth.AuthScheme;
        import org.apache.commons.httpclient.auth.CredentialsProvider;
        import org.apache.commons.httpclient.auth.CredentialsNotAvailableException;
        import org.apache.commons.httpclient.auth.NTLMScheme;
        import org.apache.commons.httpclient.auth.RFC2617Scheme;
        import org.apache.commons.httpclient.methods.GetMethod;
        
        /**
         * A simple example that uses HttpClient to perform interactive
         * authentication.
         *
         * @author Oleg Kalnichevski
         */
        public class InteractiveAuthenticationExample {
        
            /**
             * Constructor for InteractiveAuthenticationExample.
             */
            public InteractiveAuthenticationExample() {
                super();
            }
        
            public static void main(String[] args) throws Exception {
        
                InteractiveAuthenticationExample demo = new InteractiveAuthenticationExample();
                demo.doDemo();
            }
            
            private void doDemo() throws IOException {
        
                HttpClient client = new HttpClient();
                client.getParams().setParameter(
                    CredentialsProvider.PROVIDER, new ConsoleAuthPrompter());
                GetMethod httpget = new GetMethod("http://target-host/requires-auth.html");
                httpget.setDoAuthentication(true);
                try {
                    // execute the GET
                    int status = client.executeMethod(httpget);
                    // print the status and response
                    System.out.println(httpget.getStatusLine().toString());
                    System.out.println(httpget.getResponseBodyAsString());
                } finally {
                    // release any connection resources used by the method
                    httpget.releaseConnection();
                }
            }
        
            public class ConsoleAuthPrompter implements CredentialsProvider {
        
                private BufferedReader in = null; 
                public ConsoleAuthPrompter() {
                    super();
                    this.in = new BufferedReader(new InputStreamReader(System.in));
                }
                
                private String readConsole() throws IOException {
                    return this.in.readLine();
                }
                
                public Credentials getCredentials(
                    final AuthScheme authscheme, 
                    final String host, 
                    int port, 
                    boolean proxy)
                    throws CredentialsNotAvailableException 
                {
                    if (authscheme == null) {
                        return null;
                    }
                    try{
                        if (authscheme instanceof NTLMScheme) {
                            System.out.println(host + ":" + port + " requires Windows authentication");
                            System.out.print("Enter domain: ");
                            String domain = readConsole();   
                            System.out.print("Enter username: ");
                            String user = readConsole();   
                            System.out.print("Enter password: ");
                            String password = readConsole();
                            return new NTCredentials(user, password, host, domain);    
                        } else
                        if (authscheme instanceof RFC2617Scheme) {
                            System.out.println(host + ":" + port + " requires authentication with the realm '" 
                                + authscheme.getRealm() + "'");
                            System.out.print("Enter username: ");
                            String user = readConsole();   
                            System.out.print("Enter password: ");
                            String password = readConsole();
                            return new UsernamePasswordCredentials(user, password);    
                        } else {
                            throw new CredentialsNotAvailableException("Unsupported authentication scheme: " +
                                authscheme.getSchemeName());
                        }
                    } catch (IOException e) {
                        throw new CredentialsNotAvailableException(e.getMessage(), e);
                    }
                }
            }
        }
        
    