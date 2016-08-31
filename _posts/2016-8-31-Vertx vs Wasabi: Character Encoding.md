---
layout: post
title: Vertx vs Wasabi - Character Encoding
category: 'technology'
---

Vert.x is a powerful application framework, can be used in Kotlin environment.

Wasabifx is an application framework for Kotlin.


##  1, Vert.x server: http://localhost:8080

Server side:

```
val server = vertx.createHttpServer()
val router = Router.router(vertx)

router.get("/contact").handler(findContactHandler)
router.get("/api/searchcontact").handler(searchContactHandler)

server.requestHandler {
        router.accept(it)
    }.listen(8080, { handler ->
        if (!handler.succeeded()) {
            logger.error("Failed to listen on port $serverPort!")
        }
    })

val findContactHandler: (RoutingContext) -> Unit = { ctx ->
    val name = ctx.request().getParam("name")
    val contactP = contactService.findContactByName(name)

    contactP.success { info ->
        ctx.response().end(info.toString())
    }
}

val searchContactHandler: (RoutingContext) -> Unit = { ctx ->
    val name = ctx.request().getParam("name")
    val contactP = contactService.findContactByName(name)

    contactP.success { info ->
        val map = HashMap<String, Any>()
        map.put("error",false)
        map.put("results",info)

        val tc = DateTypeConverter()
        val gson = GsonBuilder().registerTypeAdapter(Date::class.java, tc).create()
        val results = gson.toJson(map)

        ctx.response().end(results)
    }
}

```

Client side:

```
    fun searchContact(name: String): Promise<Contact, Exception> = task {
        val url = "http://localhost:8080/api/searchcontact?name=$name"

        val client = OkHttpClient()
        val request = Request.Builder().url(url).get().build()

        val response = client.newCall(request).execute()
        val jsonStr = response.body().string()
        val json = JsonParser().parse(jsonStr).obj["results"]

        val der = DateTypeConverter()
        val gson = GsonBuilder().registerTypeAdapter(Date::class.java, der).create()
        gson.fromJson<Contact>(json, Contact::class.java)
    }
```

Test with browser: http://localhost:8080/contact?name=科特林, the result is ok.

Test with client program: searchContact("科特林"), the result is correct.

Conclusion: Vert.x framework is correct.


##  2, Wasabifx server: http://localhost:1234

Server side:

```
    val appConfig = AppConfiguration(1234, "My Wasabi api")
    val server = AppServer(appConfig)
    server.serveStaticFilesFromFolder("web")

    server.get("/member", findMember)
    server.post("/member", searchMember)

    server.start()

//name=科特林
//[GET] - /member?name=%E7%A7%91%E7%89%B9%E6%9E%97
val findMember = routeHandler {
    try {
        val name = request.queryParams["name"]!!
        val dao = MemberDaoImpl()

        log.info("name:" + name)
        //name:%E7%A7%91%E7%89%B9%E6%9E%97

        val member = dao.getMemberByName(name)!!
        map.put("error", false)
        map.put("results", member)
        response.send(map, "application/json")
    } catch (e: Exception) {
        map.put("error", true)
        map.put("results", e.toString())
        response.send(map, "application/json")
    }
}

//name=科特林
//[POST] - /member
val searchMember = routeHandler {
    try {
        val name = request.bodyParams["name"]!! as String
        val dao = MemberDaoImpl()

        log.info("name:" + name)
        //name:科特林

        val member = dao.getMemberByName(name)!!
        map.put("error", false)
        map.put("results", member)
        response.send(map, "application/json")
    } catch (e: Exception) {
        map.put("error", true)
        map.put("results", e.toString())
        response.send(map, "application/json")
    }
}

```

Client side:

```
    //name=科特林
    fun findMemberByNameGET(name: String): Promise<Member, Exception> = task {
        val url = "http://localhost:1234/member?name=$name"
        val client = OkHttpClient()
        val request = Request.Builder().url(url).get().build()

        val response = client.newCall(request).execute()
        val jsonStr = response.body().string()
        val json = JsonParser().parse(jsonStr).obj["results"]
        val der = DateTypeConverter()
        val gson = GsonBuilder().registerTypeAdapter(Date::class.java, der).create()
        gson.fromJson<Member>(json, Member::class.java)
    }

    //name=科特林
    fun searchMemberByNamePOST(name: String): Promise<Member, Exception> = task {
        val url = "http://localhost:1234/member"
        val formBody = FormBody.Builder().add("name", name).build()
        val client = OkHttpClient()
        val request = Request.Builder().url(url).post(formBody).build()

        val response = client.newCall(request).execute()
        val jsonStr = response.body().string()
        val json = JsonParser().parse(jsonStr).obj["results"]
        val der = DateTypeConverter()
        val gson = GsonBuilder().registerTypeAdapter(Date::class.java, der).create()
        gson.fromJson<Member>(json, Member::class.java)
    }

```

Test with client code, when do GET request, search string "科特林" in console output is : %E7%A7%91%E7%89%B9%E6%9E%97,
did not hit the record in mysql.

When do POST request, search string "科特林" in console output is : 科特林, hit the record in mysql.



