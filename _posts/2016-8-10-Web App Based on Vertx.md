---
layout: post
title: Web App Based on Vert.x
category: 'technology'
---

Vert.x is not based on Servlets, which makes it a good choice for people without Java background, especially Web developers. The fact that Vert.x comes with an embedded Web server enables simple deployment and easy integration with frontend tools.

##  MainApp

```
class MainApp : AbstractVerticle() {

    override fun start() {
        val server = vertx.createHttpServer()
        val router = Router.router(vertx)

        router.get("/about").handler{ ctx ->
            ctx.response().end("about my web app")
        }

        server.requestHandler {
            router.accept(it)
        }.listen(8080, { handler ->
              if (!handler.succeeded()) {
                    logger.error("Failed to listen on port 8080!")
              }
        })
    }

    override fun stop() {
       System.out.println("Server stopped.")
    }

}
```

##  Router & Route

```
val router = Router.router(vertx)

router.route().handler(CookieHandler.create())
router.route().handler(SessionHandler.create(LocalSessionStore.create(vertx)))
router.route().handler(UserSessionHandler.create(authProvider))
router.route("/hidden/*").handler(RedirectAuthHandler.create(authProvider))
router.route("/login").handler(BodyHandler.create());
router.route("/login").handler(FormLoginHandler.create(authProvider))
router.route("/public/*").handler(staticHandler)

router.get("/hidden/admin").handler { ctx ->
    ////
}

router.get("/members").handler(getMembersPageRouteHandler)

router.post("/member").handler(....)

router.put("/member").handler(....)

router.patch("/member").handler(...)

router.delete("/member/:id").handler(...)

```

##  RequestHandler

form one:
```
router.get("/about").handler(myHander)

val myHandler:(RoutingContext) -> Unit = { ctx ->
    ctx.response().end("about my web app")
}
```

form two:

```
router.get("/about").handler{ ctx ->
    ctx.response().end("About kotlin")
}
```

## Thymeleaf

```
val templateEngine = ThymeleafTemplateEngine.create()

router.get("/about").handler{ ctx ->
    ctx.put("name","kotlin")
    templateEngine.render(ctx, "public/templates/about.html",{ buf ->
        if (buf.failed()) {
            logger.error("Template rendering failed:" + buf.cause())
        } else {
            val response = ctx.response()
            response.end(buf.result())
        }

    }
}

```

