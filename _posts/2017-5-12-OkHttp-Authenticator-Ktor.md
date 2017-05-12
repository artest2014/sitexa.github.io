---
layout: post
title: OkHttp Authenticator in Ktor
category: 'technology'
---

Ktor提供了多种认证机制，Basic,OAuth1a,OAuth2. 测试一种简单的认证机制BasicAuthentication,使用场景是
AppClient访问AppServer时，需要进行认证。通常是登记一个AppID,分配一个AppKey.客户端在请求中携带这一对字
符串，服务端用其与数据库中保存的认证串比对以进行核实。

##  服务端

Ktor有一个类UserHashedTableAuth(Map<String,ByteArray>,Digester)，Map<String,ByteArray>是name,password
健值对，是保存在服务端的用户名和密码对。该类有一处方法authenticate(UserPasswordCredential),返回值是UserIdPrincipal.

```
val hashedUserTable = UserHashedTableAuth(table = mapOf(
        "appId" to decodeBase64("VltM4nfheqcJSyH887H+4NEOm2tDuKCl83p5axYXlF0=") // sha256 for "appkey"
))

authentication { basicAuthentication("ktor") { hashedUserTable.authenticate(it) } }
 
```
普通表单(contentType:application/form-data)可以通过class Download(val id:Int)来接收表单项，
文件表单(multipart/form-data)不能通过class Upload接收表单项，这些表单项(FormItem,FileItem)需要从multipart中解码出来.


##  客户端

第一步，定义Authenticator实例，写入Credential,将其放进request的header里面；
第二步，创建客户端，okClient,放入authenticator.
第三步，发送请求到服务端，如果认证错误，则请求不到所需要的数据，如果通过认证，则执行请求的动作。

``` 

val authenticator = Authenticator { _, response ->
    fun responseCount(response: Response): Int {
        var result = 1
        while ((response.priorResponse()) != null) result++
        return result
    }

    if (responseCount(response) >= 3) return@Authenticator null

    val credential = Credentials.basic("appId", "appKey")
    response.request().newBuilder().header("Authorization", credential).build()
}

val okClient = OkHttpClient().newBuilder()
            .authenticator(authenticator)
            .build()

val retrofit = Retrofit.Builder()
            .baseUrl(apiBaseUrl)
            .client(okClient)
            .addConverterFactory(GsonConverterFactory.create())
            .build()

private val sweetApi = retrofit.create(SweetApi::class.java)

fun getSweet(id: Int): Sweet = sweetApi.singleSweet(id).execute().body()

val sweet = getSweet(id:Int)

```
