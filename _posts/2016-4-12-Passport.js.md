---
layout: post
title: Passport.js - Simple, unobtrusive authentication for Node.js
category: 'technology'
---

Passport is authentication middleware for Node.js. Extremely flexible and modular, Passport can be unobtrusively dropped in to any Express-based web application. A comprehensive set of strategies support authentication using a username and password, Facebook, Twitter, and more.

##Overview

Passport is authentication middleware for Node. It is designed to serve a singular purpose: authenticate requests. When writing modules, encapsulation is a virtue, so Passport delegates all other functionality to the application. This separation of concerns keeps code clean and maintainable, and makes Passport extremely easy to integrate into an application.

In modern web applications, authentication can take a variety of forms. Traditionally, users log in by providing a username and password. With the rise of social networking, single sign-on using an OAuth provider such as Facebook or Twitter has become a popular authentication method. Services that expose an API often require token-based credentials to protect access.

Passport recognizes that each application has unique authentication requirements. Authentication mechanisms, known as strategies, are packaged as individual modules. Applications can choose which strategies to employ, without creating unnecessary dependencies.

Despite the complexities involved in authentication, code does not have to be complicated.

    app.post('/login', passport.authenticate('local', { successRedirect: '/',failureRedirect: '/login' }));
    
##Authenticate

    app.post('/login',
      passport.authenticate('local'),
      function(req, res) {
        // If this function gets called, authentication was successful.
        // `req.user` contains the authenticated user.
        res.redirect('/users/' + req.user.username);
      });
      
###Redirects

    app.post('/login',
      passport.authenticate('local', { successRedirect: '/',failureRedirect: '/login' }));
  
###Flash Messages
  
    app.post('/login',
      passport.authenticate('local', { successRedirect: '/',
                                       failureRedirect: '/login',
                                       failureFlash: true })
    );
    
    passport.authenticate('local', { failureFlash: 'Invalid username or password.' });
    
    passport.authenticate('local', { successFlash: 'Welcome!' });
        
###Disable Sessions
        
    app.get('/api/users/me',
      passport.authenticate('basic', { session: false }),
      function(req, res) {
        res.json({ id: req.user.id, username: req.user.username });
      });
      
###Custom Callback
      
    app.get('/login', function(req, res, next) {
      passport.authenticate('local', function(err, user, info) {
        if (err) { return next(err); }
        if (!user) { return res.redirect('/login'); }
        req.logIn(user, function(err) {
          if (err) { return next(err); }
          return res.redirect('/users/' + user.username);
        });
      })(req, res, next);
    });
    
##Configure
    
Three pieces need to be configured to use Passport for authentication:
    
-    Authentication strategies
-    Application middleware
-    Sessions (optional)

###Strategies
   
    var passport = require('passport')
      , LocalStrategy = require('passport-local').Strategy;
    
    passport.use(new LocalStrategy(
      function(username, password, done) {
        User.findOne({ username: username }, function (err, user) {
          if (err) { return done(err); }
          if (!user) {
            return done(null, false, { message: 'Incorrect username.' });
          }
          if (!user.validPassword(password)) {
            return done(null, false, { message: 'Incorrect password.' });
          }
          return done(null, user);
        });
      }
    ));
    
###Verify Callback
    
    return done(null, user);
    return done(null, false);
    return done(null, false, { message: 'Incorrect password.' });
    return done(err);
    
###Middleware
    
In a Connect or Express-based application, passport.initialize() middleware is required to initialize Passport. If your application uses persistent login sessions, passport.session() middleware must also be used.
    
    app.configure(function() {
      app.use(express.static('public'));
      app.use(express.cookieParser());
      app.use(express.bodyParser());
      app.use(express.session({ secret: 'keyboard cat' }));
      app.use(passport.initialize());
      app.use(passport.session());
      app.use(app.router);
    });
        
Note that enabling session support is entirely optional, though it is recommended for most applications. If enabled, be sure to use express.session() before passport.session() to ensure that the login session is restored in the correct order.

###Sessions

In a typical web application, the credentials used to authenticate a user will only be transmitted during the login request. If authentication succeeds, a session will be established and maintained via a cookie set in the user's browser.

Each subsequent request will not contain credentials, but rather the unique cookie that identifies the session. In order to support login sessions, Passport will serialize and deserialize user instances to and from the session.

    passport.serializeUser(function(user, done) {
      done(null, user.id);
    });
    
    passport.deserializeUser(function(id, done) {
      User.findById(id, function(err, user) {
        done(err, user);
      });
    });
            
##Username & Password

The most widely used way for websites to authenticate users is via a username and password. Support for this mechanism is provided by the passport-local module.

###Install

    $ npm install passport-local
    
###Configuration
    
    var passport = require('passport')
      , LocalStrategy = require('passport-local').Strategy;
    
    passport.use(new LocalStrategy(
      function(username, password, done) {
        User.findOne({ username: username }, function(err, user) {
          if (err) { return done(err); }
          if (!user) {
            return done(null, false, { message: 'Incorrect username.' });
          }
          if (!user.validPassword(password)) {
            return done(null, false, { message: 'Incorrect password.' });
          }
          return done(null, user);
        });
      }
    ));    
    
###Form

    <form action="/login" method="post">
        <div>
            <label>Username:</label>
            <input type="text" name="username"/>
        </div>
        <div>
            <label>Password:</label>
            <input type="password" name="password"/>
        </div>
        <div>
            <input type="submit" value="Log In"/>
        </div>
    </form>
    
###Route
    
    app.post('/login',
      passport.authenticate('local', { successRedirect: '/',
                                       failureRedirect: '/login',
                                       failureFlash: true })
    );
    
###Parameters
    
    passport.use(new LocalStrategy({
        usernameField: 'email',
        passwordField: 'passwd'
      },
      function(username, password, done) {
        // ...
      }
    ));
    
##OpenID
    
OpenID is an open standard for federated authentication. When visiting a website, users present their OpenID to sign in. The user then authenticates with their chosen OpenID provider, which issues an assertion to confirm the user's identity. The website verifies this assertion in order to sign the user in.

Support for OpenID is provided by the passport-openid module.
    
###Install

    $ npm install passport-openid
    
###Configuration
    
    var passport = require('passport')
      , OpenIDStrategy = require('passport-openid').Strategy;
    
    passport.use(new OpenIDStrategy({
        returnURL: 'http://www.example.com/auth/openid/return',
        realm: 'http://www.example.com/'
      },
      function(identifier, done) {
        User.findOrCreate({ openId: identifier }, function(err, user) {
          done(err, user);
        });
      }
    ));
    
###Form
    
    <form action="/auth/openid" method="post">
        <div>
            <label>OpenID:</label>
            <input type="text" name="openid_identifier"/><br/>
        </div>
        <div>
            <input type="submit" value="Sign In"/>
        </div>
    </form>
    
###Routes

    // Accept the OpenID identifier and redirect the user to their OpenID
    // provider for authentication.  When complete, the provider will redirect
    // the user back to the application at:
    //     /auth/openid/return
    app.post('/auth/openid', passport.authenticate('openid'));
    
    // The OpenID provider has redirected the user back to the application.
    // Finish the authentication process by verifying the assertion.  If valid,
    // the user will be logged in.  Otherwise, authentication has failed.
    app.get('/auth/openid/return',
      passport.authenticate('openid', { successRedirect: '/',
                                        failureRedirect: '/login' }));
                                        
###Profile Exchange

    passport.use(new OpenIDStrategy({
        returnURL: 'http://www.example.com/auth/openid/return',
        realm: 'http://www.example.com/',
        profile: true
      },
      function(identifier, profile, done) {
        // ...
      }
    ));
    
##OAuth
    
OAuth is a standard protocol that allows users to authorize API access to web and desktop or mobile applications. Once access has been granted, the authorized application can utilize the API on behalf of the user. OAuth has also emerged as a popular mechanism for delegated authentication.
    
The initial version of OAuth was developed as an open standard by a loosely organized collective of web developers. Their work resulted in OAuth 1.0, which was superseded by OAuth 1.0a. This work has now been standardized by the IETF as RFC 5849.

Recent efforts undertaken by the Web Authorization Protocol Working Group have focused on defining OAuth 2.0. Due to the lengthy standardization effort, providers have proceeded to deploy implementations conforming to various drafts, each with slightly different semantics.
    
Support for OAuth is provided by the passport-oauth module.
    
###Install
    
    $ npm install passport-oauth
    
###OAuth 1.0
    
###Configuration    
    
    var passport = require('passport')
      , OAuthStrategy = require('passport-oauth').OAuthStrategy;
    
    passport.use('provider', new OAuthStrategy({
        requestTokenURL: 'https://www.provider.com/oauth/request_token',
        accessTokenURL: 'https://www.provider.com/oauth/access_token',
        userAuthorizationURL: 'https://www.provider.com/oauth/authorize',
        consumerKey: '123-456-789',
        consumerSecret: 'shhh-its-a-secret'
        callbackURL: 'https://www.example.com/auth/provider/callback'
      },
      function(token, tokenSecret, profile, done) {
        User.findOrCreate(..., function(err, user) {
          done(err, user);
        });
      }
    ));    
    
###Routes
    
    // Redirect the user to the OAuth provider for authentication.  When
    // complete, the provider will redirect the user back to the application at
    //     /auth/provider/callback
    app.get('/auth/provider', passport.authenticate('provider'));
    
    // The OAuth provider has redirected the user back to the application.
    // Finish the authentication process by attempting to obtain an access
    // token.  If authorization was granted, the user will be logged in.
    // Otherwise, authentication has failed.
    app.get('/auth/provider/callback',
        passport.authenticate('provider', { successRedirect: '/',
                                          failureRedirect: '/login' }));
                                          
###Link

    <a href="/auth/provider">Log In with OAuth Provider</a>
    
##OAuth 2.0

OAuth 2.0 is the successor to OAuth 1.0, and is designed to overcome perceived shortcomings in the earlier version. The authentication flow is essentially the same. The user is first redirected to the service provider to authorize access. After authorization has been granted, the user is redirected back to the application with a code that can be exchanged for an access token. The application requesting access, known as a client, is identified by an ID and secret.

###Configuration

When using the generic OAuth 2.0 strategy, the client ID, client secret, and endpoints are specified as options.

    var passport = require('passport')
      , OAuth2Strategy = require('passport-oauth').OAuth2Strategy;
    
    passport.use('provider', new OAuth2Strategy({
        authorizationURL: 'https://www.provider.com/oauth2/authorize',
        tokenURL: 'https://www.provider.com/oauth2/token',
        clientID: '123-456-789',
        clientSecret: 'shhh-its-a-secret'
        callbackURL: 'https://www.example.com/auth/provider/callback'
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate(..., function(err, user) {
          done(err, user);
        });
      }
    ));
    
###Routes
    
    // Redirect the user to the OAuth 2.0 provider for authentication.  When
    // complete, the provider will redirect the user back to the application at
    //     /auth/provider/callback
    app.get('/auth/provider', passport.authenticate('provider'));
    
    // The OAuth 2.0 provider has redirected the user back to the application.
    // Finish the authentication process by attempting to obtain an access
    // token.  If authorization was granted, the user will be logged in.
    // Otherwise, authentication has failed.
    app.get('/auth/provider/callback',
      passport.authenticate('provider', { successRedirect: '/',
                                          failureRedirect: '/login' }));
                                              
###Scope

    app.get('/auth/provider',
      passport.authenticate('provider', { scope: 'email' })
    );
    
    app.get('/auth/provider',
      passport.authenticate('provider', { scope: ['email', 'sms'] })
    );
    
###Link

    <a href="/auth/provider">Log In with OAuth 2.0 Provider</a>
    
##User Profile

-    provider {String}
     The provider with which the user authenticated (facebook, twitter, etc.).
-    id {String}
    A unique identifier for the user, as generated by the service provider.
-    displayName {String}
    The name of this user, suitable for display.
-    name {Object}
    -   familyName {String}
        The family name of this user, or "last name" in most Western languages.
    -   givenName {String}
        The given name of this user, or "first name" in most Western languages.
    -   middleName {String}
        The middle name of this user.
-   emails {Array} [n]
    -   value {String}
    The actual email address.
    -   type {String}
        The type of email address (home, work, etc.).
-    photos {Array} [n]
    -   value {String}
        The URL of the image.

##Facebook

The Facebook strategy allows users to log in to a web application using their Facebook account. Internally, Facebook authentication works using OAuth 2.0.

Support for Facebook is implemented by the passport-facebook module.

###Install

    $ npm install passport-facebook
    
###Configuration

    var passport = require('passport')
      , FacebookStrategy = require('passport-facebook').Strategy;
    
    passport.use(new FacebookStrategy({
        clientID: FACEBOOK_APP_ID,
        clientSecret: FACEBOOK_APP_SECRET,
        callbackURL: "http://www.example.com/auth/facebook/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate(..., function(err, user) {
          if (err) { return done(err); }
          done(null, user);
        });
      }
    ));
    
###Routes

    // Redirect the user to Facebook for authentication.  When complete,
    // Facebook will redirect the user back to the application at
    //     /auth/facebook/callback
    app.get('/auth/facebook', passport.authenticate('facebook'));
    
    // Facebook will redirect the user to this URL after approval.  Finish the
    // authentication process by attempting to obtain an access token.  If
    // access was granted, the user will be logged in.  Otherwise,
    // authentication has failed.
    app.get('/auth/facebook/callback',
      passport.authenticate('facebook', { successRedirect: '/',
                                          failureRedirect: '/login' }));
                                          
###Permissions

    app.get('/auth/facebook',
      passport.authenticate('facebook', { scope: 'read_stream' })
    );
    
    app.get('/auth/facebook',
      passport.authenticate('facebook', { scope: ['read_stream', 'publish_actions'] })
    );
    
###Link

    <a href="/auth/facebook">Login with Facebook</a>
    
##Twitter

The Twitter strategy allows users to sign in to a web application using their Twitter account. Internally, Twitter authentication works using OAuth 1.0a.

Support for Twitter is implemented by the passport-twitter module.

###Install

    $ npm install passport-twitter
    
###Configuration

    var passport = require('passport')
      , TwitterStrategy = require('passport-twitter').Strategy;
    
    passport.use(new TwitterStrategy({
        consumerKey: TWITTER_CONSUMER_KEY,
        consumerSecret: TWITTER_CONSUMER_SECRET,
        callbackURL: "http://www.example.com/auth/twitter/callback"
      },
      function(token, tokenSecret, profile, done) {
        User.findOrCreate(..., function(err, user) {
          if (err) { return done(err); }
          done(null, user);
        });
      }
    ));
    
###Routes

    // Redirect the user to Twitter for authentication.  When complete, Twitter
    // will redirect the user back to the application at
    //   /auth/twitter/callback
    app.get('/auth/twitter', passport.authenticate('twitter'));
    
    // Twitter will redirect the user to this URL after approval.  Finish the
    // authentication process by attempting to obtain an access token.  If
    // access was granted, the user will be logged in.  Otherwise,
    // authentication has failed.
    app.get('/auth/twitter/callback',
      passport.authenticate('twitter', { successRedirect: '/',
                                         failureRedirect: '/login' }));
                                         
###Link

    <a href="/auth/twitter">Sign in with Twitter</a>
    
##Google
    
The Google strategy allows users to sign in to a web application using their Google account. Google used to support OpenID internally, but it now works based on OpenID Connect and supports oAuth 1.0 and oAuth 2.0.

Support for Google is implemented by the passport-google-oauth module.

###Install

    $ npm install passport-google-oauth
    
###Configuration
    
####oAuth 1.0 - Configuration

    var passport = require('passport');
    var GoogleStrategy = require('passport-google-oauth').OAuthStrategy;
    
    // Use the GoogleStrategy within Passport.
    //   Strategies in passport require a `verify` function, which accept
    //   credentials (in this case, a token, tokenSecret, and Google profile), and
    //   invoke a callback with a user object.
    passport.use(new GoogleStrategy({
        consumerKey: GOOGLE_CONSUMER_KEY,
        consumerSecret: GOOGLE_CONSUMER_SECRET,
        callbackURL: "http://www.example.com/auth/google/callback"
      },
      function(token, tokenSecret, profile, done) {
          User.findOrCreate({ googleId: profile.id }, function (err, user) {
            return done(err, user);
          });
      }
    ));
    
####oAuth 1.0 - Routes
   
    // GET /auth/google
    //   Use passport.authenticate() as route middleware to authenticate the
    //   request.  The first step in Google authentication will involve redirecting
    //   the user to google.com.  After authorization, Google will redirect the user
    //   back to this application at /auth/google/callback
    app.get('/auth/google',
      passport.authenticate('google', { scope: 'https://www.google.com/m8/feeds' });
    
    // GET /auth/google/callback
    //   Use passport.authenticate() as route middleware to authenticate the
    //   request.  If authentication fails, the user will be redirected back to the
    //   login page.  Otherwise, the primary route function function will be called,
    //   which, in this example, will redirect the user to the home page.
    app.get('/auth/google/callback', 
      passport.authenticate('google', { failureRedirect: '/login' }),
      function(req, res) {
        res.redirect('/');
      });
      
####oAuth 2.0 - Configuration

    var passport = require('passport');
    var GoogleStrategy = require('passport-google-oauth').OAuth2Strategy;
    
    // Use the GoogleStrategy within Passport.
    //   Strategies in Passport require a `verify` function, which accept
    //   credentials (in this case, an accessToken, refreshToken, and Google
    //   profile), and invoke a callback with a user object.
    passport.use(new GoogleStrategy({
        clientID: GOOGLE_CLIENT_ID,
        clientSecret: GOOGLE_CLIENT_SECRET,
        callbackURL: "http://www.example.com/auth/google/callback"
      },
      function(accessToken, refreshToken, profile, done) {
           User.findOrCreate({ googleId: profile.id }, function (err, user) {
             return done(err, user);
           });
      }
    ));
    

####oAuth 2.0 - Routes

    // GET /auth/google
    //   Use passport.authenticate() as route middleware to authenticate the
    //   request.  The first step in Google authentication will involve
    //   redirecting the user to google.com.  After authorization, Google
    //   will redirect the user back to this application at /auth/google/callback
    app.get('/auth/google',
      passport.authenticate('google', { scope: ['https://www.googleapis.com/auth/plus.login'] }));
    
    // GET /auth/google/callback
    //   Use passport.authenticate() as route middleware to authenticate the
    //   request.  If authentication fails, the user will be redirected back to the
    //   login page.  Otherwise, the primary route function function will be called,
    //   which, in this example, will redirect the user to the home page.
    app.get('/auth/google/callback', 
      passport.authenticate('google', { failureRedirect: '/login' }),
      function(req, res) {
        res.redirect('/');
      });
      
###Link

    <a href="/auth/google">Sign In with Google</a>
    
    
##Basic & Digest

Along with defining HTTP's authentication framework, RFC 2617 also defined the Basic and Digest authentications schemes. These two schemes both use usernames and passwords as credentials to authenticate users, and are often used to protect API endpoints.

It should be noted that relying on username and password creditials can have adverse security impacts, especially in scenarios where there is not a high degree of trust between the server and client. In these situations, it is recommended to use an authorization framework such as OAuth 2.0.

Support for Basic and Digest schemes is provided by the passport-http module.

###Install

    $ npm install passport-http
    
###Basic - Configuration
    
    passport.use(new BasicStrategy(
      function(username, password, done) {
        User.findOne({ username: username }, function (err, user) {
          if (err) { return done(err); }
          if (!user) { return done(null, false); }
          if (!user.validPassword(password)) { return done(null, false); }
          return done(null, user);
        });
      }
    ));
    
###Basic - Protect Endpoints

    app.get('/api/me',
      passport.authenticate('basic', { session: false }),
      function(req, res) {
        res.json(req.user);
      });
      
###Digest - Configuration

    passport.use(new DigestStrategy({ qop: 'auth' },
      function(username, done) {
        User.findOne({ username: username }, function (err, user) {
          if (err) { return done(err); }
          if (!user) { return done(null, false); }
          return done(null, user, user.password);
        });
      },
      function(params, done) {
        // validate nonces as necessary
        done(null, true)
      }
    ));
    
###Digest - Protect Endpoints

    app.get('/api/me',
      passport.authenticate('digest', { session: false }),
      function(req, res) {
        res.json(req.user);
      });
      
##OAuth

OAuth (formally specified by RFC 5849) provides a means for users to grant third-party applications access to their data without exposing their password to those applications.

The protocol greatly improves the security of web applications, in particular, and OAuth has been important in bringing attention to the potential dangers of exposing passwords to external services.

While OAuth 1.0 is still widely used, it has been superseded by OAuth 2.0. It is recommended to base new implementations on OAuth 2.0.

When using OAuth to protect API endpoints, there are three distinct steps that that must be performed:

-   The application requests permission from the user for access to protected resources.
-   A token is issued to the application, if permission is granted by the user.
-   The application authenticates using the token to access protected resources.

Once issued, OAuth tokens can be authenticated using the passport-http-oauth module.

###Install
   
    $ npm install passport-http-oauth
    
###Configuration

    passport.use('token', new TokenStrategy(
      function(consumerKey, done) {
        Consumer.findOne({ key: consumerKey }, function (err, consumer) {
          if (err) { return done(err); }
          if (!consumer) { return done(null, false); }
          return done(null, consumer, consumer.secret);
        });
      },
      function(accessToken, done) {
        AccessToken.findOne({ token: accessToken }, function (err, token) {
          if (err) { return done(err); }
          if (!token) { return done(null, false); }
          Users.findById(token.userId, function(err, user) {
            if (err) { return done(err); }
            if (!user) { return done(null, false); }
            // fourth argument is optional info.  typically used to pass
            // details needed to authorize the request (ex: `scope`)
            return done(null, user, token.secret, { scope: token.scope });
          });
        });
      },
      function(timestamp, nonce, done) {
        // validate the timestamp and nonce as necessary
        done(null, true)
      }
    ));
    
###Protect Endpoints

    app.get('/api/me',
      passport.authenticate('token', { session: false }),
      function(req, res) {
        res.json(req.user);
      });
      
##OAuth 2.0

OAuth 2.0 (formally specified by RFC 6749) provides an authorization framework which allows users to authorize access to third-party applications. When authorized, the application is issued a token to use as an authentication credential. This has two primary security benefits:

-   The application does not need to store the user's username and password.
-   The token can have a restricted scope (for example: read-only access).
-   These benefits are particularly important for ensuring the security of web applications, making OAuth 2.0 the predominant standard for API authentication.

When using OAuth 2.0 to protect API endpoints, there are three distinct steps that must be performed:

-   The application requests permission from the user for access to protected resources.
-   A token is issued to the application, if permission is granted by the user.
-   The application authenticates using the token to access protected resources.

###Bearer Tokens

Bearer tokens are the most widely issued type of token in OAuth 2.0. So much so, in fact, that many implementations assume that bearer tokens are the only type of token issued.

Bearer tokens can be authenticated using the passport-http-bearer module.

###Install

    $ npm install passport-http-bearer
    
###Configuration

    passport.use(new BearerStrategy(
      function(token, done) {
        User.findOne({ token: token }, function (err, user) {
          if (err) { return done(err); }
          if (!user) { return done(null, false); }
          return done(null, user, { scope: 'read' });
        });
      }
    ));
    
###Protect Endpoints

    app.get('/api/me',
      passport.authenticate('bearer', { session: false }),
      function(req, res) {
        res.json(req.user);
      });
      
##Log In

Passport exposes a login() function on req (also aliased as logIn()) that can be used to establish a login session.
    
    req.login(user, function(err) {
      if (err) { return next(err); }
      return res.redirect('/users/' + req.user.username);
    });
    
##Log Out
    
Passport exposes a logout() function on req (also aliased as logOut()) that can be called from any route handler which needs to terminate a login session. Invoking logout() will remove the req.user property and clear the login session (if any).

    app.get('/logout', function(req, res){
      req.logout();
      res.redirect('/');
    });
    

##Authorize

An application may need to incorporate information from multiple third-party services. In this case, the application will request the user to "connect", for example, both their Facebook and Twitter accounts.

When this occurs, a user will already be authenticated with the application, and any subsequent third-party accounts merely need to be authorized and associated with the user. Because authentication and authorization in this situation are similar, Passport provides a means to accommodate both.

Authorization is performed by calling passport.authorize(). If authorization is granted, the result provided by the strategy's verify callback will be assigned to req.account. The existing login session and req.user will be unaffected.

    app.get('/connect/twitter',
      passport.authorize('twitter-authz', { failureRedirect: '/account' })
    );
    
    app.get('/connect/twitter/callback',
      passport.authorize('twitter-authz', { failureRedirect: '/account' }),
      function(req, res) {
        var user = req.user;
        var account = req.account;
    
        // Associate the Twitter account with the logged-in user.
        account.userId = user.id;
        account.save(function(err) {
          if (err) { return self.error(err); }
          self.redirect('/');
        });
      }
    );
    
###Configuration

    passport.use('twitter-authz', new TwitterStrategy({
        consumerKey: TWITTER_CONSUMER_KEY,
        consumerSecret: TWITTER_CONSUMER_SECRET,
        callbackURL: "http://www.example.com/connect/twitter/callback"
      },
      function(token, tokenSecret, profile, done) {
        Account.findOne({ domain: 'twitter.com', uid: profile.id }, function(err, account) {
          if (err) { return done(err); }
          if (account) { return done(null, account); }
    
          var account = new Account();
          account.domain = 'twitter.com';
          account.uid = profile.id;
          var t = { kind: 'oauth', token: token, attributes: { tokenSecret: tokenSecret } };
          account.tokens.push(t);
          return done(null, account);
        });
      }
    ));
    
###Association in Verify Callback

    passport.use(new TwitterStrategy({
        consumerKey: TWITTER_CONSUMER_KEY,
        consumerSecret: TWITTER_CONSUMER_SECRET,
        callbackURL: "http://www.example.com/auth/twitter/callback",
        passReqToCallback: true
      },
      function(req, token, tokenSecret, profile, done) {
        if (!req.user) {
          // Not logged-in. Authenticate based on Twitter account.
        } else {
          // Logged in. Associate Twitter account with user.  Preserve the login
          // state by supplying the existing user after association.
          // return done(null, req.user);
        }
      }
    ));
    

