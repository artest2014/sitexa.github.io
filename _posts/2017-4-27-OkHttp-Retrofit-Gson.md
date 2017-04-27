---
layout: post
title: OkHttp, Retrofit, Gson
category: 'technology'
---


Gson组件配合OkHttp,Retrofit在网络访问对Json串进行转化时，与Moshi组件有区别。前者是在组件内容进行的，
后者是在组件外部进行的。从编码角度看，Moshi很简单；从代码的优雅度看，Gson更胜一筹。Moshi的TypeAdapter
写法简单明了，而Gson的TypeAdapter就要复杂得多。下面代码中，JodaTimeAdapter是Moshi写法，JodaTypeAdapter
是Gson写法。结合本文与上一文，对照一下两者的区别。


##  OkHttp,Retrofit,Gson组合

看这段代码：

```

interface UserApi {
    @GET("/sweet/{id}")
    fun sweet2(@Path("id") id: Int): Call<Sweet>

    @GET("/user/{userId}")
    fun userPage2(@Path("userId") userId:String):Call<List<Sweet>>
}

class JodaTimeAdapter {
    @ToJson
    fun toJson(date: DateTime) = date.millis

    @FromJson
    fun fromJson(json: Long) = DateTime(json)
}

class JodaTypeAdapter : JsonSerializer<DateTime>, JsonDeserializer<DateTime> {
    override fun serialize(src: DateTime, srcType: Type, context: JsonSerializationContext): JsonElement {
        //return JsonPrimitive(src.toString())
        return JsonPrimitive(src.millis)
    }

    @Throws(JsonParseException::class)
    override fun deserialize(json: JsonElement, type: Type, context: JsonDeserializationContext): DateTime {
        try {
            return DateTime(json.asLong)
        } catch (e: IllegalArgumentException) {
            val date = context.deserialize<DateTime>(json, DateTime::class.java)
            return date
        }
    }
}

val headerInterceptor = Interceptor { chain ->
    chain.proceed(chain.request().newBuilder().addHeader("Accept", "application/json").build())
}

val loggingInterceptor = HttpLoggingInterceptor().apply { level = HttpLoggingInterceptor.Level.BODY }

fun getSweet2(id:Int):Sweet{

    val gson = GsonBuilder().
            registerTypeAdapter(DateTime::class.java,JodaTypeAdapter())
            .create()

    val okClient = OkHttpClient().newBuilder()
            .addInterceptor(headerInterceptor)
            //.addInterceptor(loggingInterceptor)
            .build()

    val retrofit = Retrofit.Builder()
            .baseUrl(BASE_URL)
            .client(okClient)
            .addConverterFactory(GsonConverterFactory.create(gson))
            .build()

    val sitexaApi = retrofit.create(UserApi::class.java)
    val call = sitexaApi.sweet2(id)

    return call.execute().body()
}

fun getUserPage2(userId: String): List<Sweet> {

    val gson = GsonBuilder()
            .registerTypeAdapter(DateTime::class.java,JodaTypeAdapter())
            .create()

    val okClient = OkHttpClient().newBuilder()
            .addInterceptor(HeaderInterceptor())
            .addInterceptor(loggingInterceptor)
            .build()

    val retrofit = Retrofit.Builder()
            .baseUrl(BASE_URL)
            .client(okClient)
            .addConverterFactory(GsonConverterFactory.create(gson))
            .build()

    val sitexaApi = retrofit.create(UserApi::class.java)
    val call = sitexaApi.userPage2(userId)
    return  call.execute().body()
}
```

-   RestFul服务接口,
-   OkHttpClient，网络访问客户端 
-   Retrofit,RestFul接口操作组件，根据接口生成实例代码，不用手工写实例代码
-   Gson,JSON转换组件
-   DateTypeAdapter,类型转换适配器


与另一文章中的Api接口的返回值类型不同：

-   上文的返回类型：Call<ResponseBody>,接口规范不明确，不知道其中对象类型；
-   本方的返回类型：Call<Sweet>,Call<List<Sweet>>，接口规范明确。


