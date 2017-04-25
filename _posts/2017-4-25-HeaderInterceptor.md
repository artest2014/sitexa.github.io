---
layout: post
title: OkHttp - add HeaderInterceptor
category: 'technology'
---

有这样的use case, 在服务端，对于 Accept = application/json的request,response将转为json.

```
intercept(ApplicationCallPipeline.Infrastructure) { call ->
            if (call.request.acceptItems().any { it.value == "application/json" }) {
                call.transform.register<JsonResponse> { value ->
                    TextContent(gson.toJson(value.data), ContentType.Application.Json)
                }
            }
        }
```

写客户端程序时，需要对请求进行定制，即添加相应的请求头HeaderInterceptor.

##  HeaderInterceptor

### Kotlin的写法：

```
class HeaderInterceptor(val name: String = "Accept", val value: String = "application/json") : Interceptor {
    override fun intercept(chain: Interceptor.Chain): Response {
        val request = chain.request().newBuilder().addHeader(name, value).build()
        return chain.proceed(request)
    }
}

val okClient = OkHttpClient().newBuilder()
            .addInterceptor(HeaderInterceptor())
            .build()

val retrofit = Retrofit.Builder()
            .baseUrl(BASE_URL)
            .client(okClient)
            .addConverterFactory(GsonConverterFactory.create())
            .build()

```
或者简单优雅的写法：
```

val okClient = OkHttpClient().newBuilder().addInterceptor { chain ->
    chain.proceed(chain.request().newBuilder().addHeader("key", "value").build())
}.build()

//or
val interceptor = Interceptor { chain ->
    chain.proceed(chain.request().newBuilder().addHeader("Accept", "application/json").build())
}

val okClient =  OkHttpClient().newBuilder().addInterceptor(interceptor).build()

val retrofit = Retrofit.Builder()
            .baseUrl(BASE_URL)
            .client(okClient)
            .addConverterFactory(GsonConverterFactory.create())
            .build()
```


有人说，addInterceptor()没有用，而要用addNetworkInterceptor()代替。可以比较一下。

### Java的写法

``` 
OkHttpClient httpClient = new OkHttpClient();

httpClient.addInterceptor(new Interceptor() {
    @Override
    public Response intercept(Chain chain) throws IOException {
        Request request = chain.request().newBuilder().addHeader("parameter", "value").build();
        return chain.proceed(request);
    }
});

Retrofit retrofit = new Retrofit.Builder()
    .addConverterFactory(GsonConverterFactory.create())
    .baseUrl(url)
    .client(httpClient)
    .build();

```

### HttpLoggingInterceptor

```
HttpLoggingInterceptor interceptor = new HttpLoggingInterceptor();
        interceptor.setLevel(HttpLoggingInterceptor.Level.BODY);
        
OkHttpClient okClient = new OkHttpClient.Builder()
                .addInterceptor(interceptor).build();
        
```