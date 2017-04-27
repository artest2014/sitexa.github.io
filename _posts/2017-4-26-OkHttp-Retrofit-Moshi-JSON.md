---
layout: post
title: OkHttp, Retrofit, Moshi and JSON
category: 'technology'
---



Square Open Source 的几个开源组件，编程接口非常简单，运行效率也非常好，特别是比较轻便。

在处理JSON对象的时候遇到过这样的问题，字段内容为长字符串，而且是文章段落，含有大量特殊字符，
比如控制字符：\n \r \t \0 等，标点符号：" ' ， 。 ； = { [ < / \ `等，还有一些非英语字符，
比如中文、日文、德文、阿拉伯文等，对JSON来说，都是合法字符，使用常用的JSON工具都能成功转换，
只要求获得的Json对象合法，即{key:value,key2:value2},key是简单字符串，value是基本类型。
不知道当key为特殊字符串时将会怎样，比如中文字符串，或者标点符号甚至控制字符，通常情况下，
是没有人那样做的。value是基本类型，比如字符串、整数、逻辑值等，不知道其他类型将会怎样。

对于字符串的处理，主要是特殊字符的处理，是大家经常遇到的问题。比如：

http://stackoverflow.com/questions/25028249/how-to-escape-special-characters-from-json-when-assign-it-to-java-string

http://stackoverflow.com/questions/3659004/json-strings-and-how-to-handle-escaped-characters?rq=1

这些讨论主要关心的是特殊字符的编码与解码(encode,decode)，或者是替代持殊字符。

我的要求是保持原始内容不变，保留一切特殊字符。因为，采用UTF-8编码时，一切特殊字符都是合法的JSON字符。

##  OkHttp,Retrofit,Moshi组合

看这段代码：

```
interface SitexaApi {
    @GET("/user/{userId}")
    fun userPage(@Path("userId") userId: String): Call<ResponseBody>

    @GET("/sweet/{id}")
    fun sweet(@Path("id") id: Int): Call<ResponseBody>
}

class JodaTimeAdapter {
    @ToJson
    fun toJson(date: DateTime) = date.millis

    @FromJson
    fun fromJson(json: Long) = DateTime(json)
}

val headerInterceptor = Interceptor { chain ->
    chain.proceed(chain.request().newBuilder().addHeader("Accept", "application/json").build())
}

val loggingInterceptor = HttpLoggingInterceptor().apply { level = HttpLoggingInterceptor.Level.BODY }

fun getSweet(id: Int): Sweet {
    val okClient = OkHttpClient().newBuilder()
            .addInterceptor(headerInterceptor)
            .addInterceptor(loggingInterceptor)
            .build()
    val retrofit = Retrofit.Builder()
            .baseUrl(BASE_URL)
            .client(okClient)
            .build()
    val sitexaApi = retrofit.create(SitexaApi::class.java)
    val call = sitexaApi.sweet(id)

    val response = call.execute()
    val jsonString = (response.body() as ResponseBody).string()

    val moshi = Moshi.Builder().add(JodaTimeAdapter()).build()
    val sweetAdapter = moshi.adapter<Sweet>(Sweet::class.java).lenient()
    val sweet = sweetAdapter.fromJson(jsonString)
    return sweet
}
```

-   RestFul服务接口
-   HeaderInterceptor,给request添加Accept=application/json头，这是服务接口的要求
-   HttpLoggingInterceptor,顾名思义，是打log用的 
-   OkHttpClient，网络访问客户端 
-   Retrofit,RestFul接口操作组件，根据接口生成实例代码，不用手工写实例代码
-   Moshi,JSON转换组件，其接口是傻瓜级的，不象Gson那样麻烦
-   JodaTimeAdapter,类型转换适配器，使用@ToJson,@FromJson注解两个方法，实现复杂类型转换，如果都是简单类型，
    就无须适配器
-   sweatAdapter,Moshi的Json转换器，负责转换JSON与对象类型

>   特别注意的是，Retrofit调用的返回值类型，如果是Any/Object,就需要进行适当的类型转换。看一些例子时，常看到
    val response = call.execute()
    val json = response.body().toString()
    因为 response.body() 是 Any/Object类型，toString()是Object.toString(),是把整个ResponseBody转化为
    字符串，而不是转换为JSON对象（本质上仍然是字符串），即key:value对。其实ResponseBody有一个string()方法，
    它能把ResponseBody转化为合法的JSON对象

另外，Kotlin号称能够实现类型的智能转换（smart cast）, 不需要显式转换，这是要通过上下文判断的。在上面的程序中，
(response.body() as ResponseBody)，如果不进行这样的显式类型转换，就没有.string()方法，而只有.toString()
方法，这是肯定要出错的。



