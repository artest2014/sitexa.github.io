---
layout: post
title: Authentication with Vert.x
category: 'technology'
---

Usually, there are several ways to authenticate a user, but here we’re going to use form-based authentication. In terms of Vert.x, it means that we will need to instantiate several built-in handlers, but most importantly we will need an AuthProvider.

The AuthProvider is an interface that has only one method - authenticate. This method will receive user credentials, and our task will be to perform password checking and send results to the sender. Since our password is stored in the database, we need the data source reference there. We can also make use of Jackson ObjectMapper, because Vert.x will pass user credentials as JSON.

##  DatabaseAuthProvider

```
class DatabaseAuthProvider(val dataSource: HikariDataSource, val jsonMapper: ObjectMapper) : AuthProvider {
    override fun authenticate(authInfoJson: JsonObject?, resultHandler: Handler<AsyncResult<User>>?) {
        val authInfo = jsonMapper.readValue(authInfoJson?.encode(), AuthInfo::class.java)
        val userT = eitherTry {
            using(sessionOf(dataSource)) { session ->
                val query = queryOf("select * from t_user where user_code = ?", authInfo.username)
                val maybeUser = query.map { DatabaseUser.fromDb(it) }.asSingle.runWithSession(session).toOption()
                maybeUser.getOrElse { throw Exception("User ${authInfo.username} not found!") }
            }
        }
        userT.fold({ exc ->
            val result = CompositeFuture.factory.failedFuture<User>(exc)
            resultHandler?.handle(result)
        }, { dbUser ->
            val isValid = BCrypt.checkpw(authInfo.password, dbUser.passwordHash)
            val result = if (isValid) {
                CompositeFuture.factory.succeededFuture(dbUser as User)
            } else {
                CompositeFuture.factory.failureFuture("Password is not valid!")
            }
            resultHandler?.handle(result)
        })
    }
}
```

##  DatabaseUser

```
class DatabaseUser(val id: UUID, val username: String, val passwordHash: String) : AbstractUser() {
  companion object {
    fun fromDb(row: Row): DatabaseUser {
      return DatabaseUser(UUID.fromString(row.string("user_id")),row.string("user_code"), row.string("password"))
    }
  }
  override fun doIsPermitted(permission: String?, resultHandler: Handler<AsyncResult<Boolean>>?) {
    val result = CompositeFuture.factory.succeededFuture(true)
    resultHandler?.handle(result)
  }

  override fun setAuthProvider(authProvider: AuthProvider?) {
  }

  override fun principal(): JsonObject {
    return JsonObject().put("username", username)
  }
}
```

Looking at these lines:

```
val userT = eitherTry {
            using(sessionOf(dataSource)) { session ->
                val query = queryOf("select * from t_user where user_code = ?", authInfo.username)
                val maybeUser = query.map { DatabaseUser.fromDb(it) }.asSingle.runWithSession(session).toOption()
                maybeUser.getOrElse { throw Exception("User ${authInfo.username} not found!") }
            }
        }
```

```val query = queryOf("select * from t_user where user_code = ?", authInfo.username)``` is a sql statement,
not using connection to database. ```query.map {DatabaseUser.fromDb(it)}``` , what is ```it```?
```DatabaseUser.fromDb(it)``` means ```it``` refers to ```Row```, but I think the query is not completed,
```runWithSession(session)``` means run query against ```session```.



##  Process

```
val authProvider = DatabaseAuthProvider(dataSource.get(), jsonMapper)
router.route("/hidden/*").handler(RedirectAuthHandler.create(authProvider))
router.route("/login").handler(BodyHandler.create());
router.route("/login").handler(FormLoginHandler.create(authProvider))
```

We’re specifying that every URL that starts with /hidden will require a user to be logged in. By default, not logged users trying to view restricted resources will be redirected to the /loginpage. After they enter their credentials, their username and password are sent to the login route via POST and FormLoginHandler sends them the AuthProvider. The FormLoginHandler requires BodyHandler, so we’adding it here.
In addition, several handlers must be assigned to route(), so they are applied to all requests:

```
router.route().handler(CookieHandler.create())
router.route().handler(SessionHandler.create(LocalSessionStore.create(vertx)))
router.route().handler(UserSessionHandler.create(authProvider))
```

These three basically maintain a session store and therefore allow logged users to use the website without having to enter their credentials all the time.





