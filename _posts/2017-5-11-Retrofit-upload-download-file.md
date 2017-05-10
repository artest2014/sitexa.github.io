---
layout: post
title: Retrofit2 upload / download file
category: 'technology'
---

在ktor框架中，使用Retrofit+OkHttp库上传／下载文件时，由于对表单的封装有很多选项，必须进行正确的选择，才能实现功能。
网络上有许多人都遇到过这一个问题，也有很多人给出了形形色色的解决办法，好象不能有效解决问题，提问的人依然层出不究。
奇怪的是官方为什么没有给出一个正确的示例。


##  服务端代码 

```

@location("/upload") class Upload

@location("/download") class Download(val id: Int)

fun Route.fileHandler(dao: DAOFacade, hashFunction: (String) -> String) {

    post<Upload> {

        var id: Int? = null
        var refId: Int? = null
        var title: String? = null
        var sortOrder: Int? = null
        var fileName: String? = null
        var fileType: String? = null

        var apiResult: ApiResult

        try {
            val multipart = call.request.receive<MultiPartData>()
            if (call.request.isMultipart()) {
                multipart.parts.forEach { part ->
                    if (part is PartData.FormItem) {
                        if (part.partName == "refId") {
                            refId = part.value.toInt()
                        } else if (part.partName == "title") {
                            title = part.value
                        } else if (part.partName == "sortOrder") {
                            sortOrder = part.value.toInt()
                        }
                    } else if (part is PartData.FileItem) {
                        val ext = File(part.originalFileName).extension
                        val file = File(uploadDir, "${System.currentTimeMillis()}.$ext")
                        part.streamProvider().use { instream ->
                            file.outputStream().buffered().use { outstream ->
                                instream.copyTo(outstream)
                            }
                        }
                        fileName = file.name
                        fileType = ContentType.fromFilePath(file.path).firstOrNull()?.contentType
                    }
                    part.dispose()
                }
            }
            id = (fileName != null).let { dao.createMedia(refId, fileName!!, fileType, title, sortOrder) }
            apiResult = ApiResult(code = ApiCode.OK, desc = "success", data = "$id")
        } catch(e: Exception) {
            apiResult = ApiResult(code = ApiCode.ERROR, desc = "fail", data = e.message!!)
        }
        call.respond(JsonResponse(apiResult))
    }

    get<Download> {
        val media = dao.getMedia(it.id)
        call.respond(LocalFileContent(File(uploadDir + "/" + media!!.fileName)))
    }
}
```
普通表单(contentType:application/form-data)可以通过class Download(val id:Int)来接收表单项，
文件表单(multipart/form-data)不能通过class Upload接收表单项，这些表单项(FormItem,FileItem)需要从multipart中解码出来.

##  Retrofit接口代码

``` 
interface FileApi {
    @Multipart @POST("/upload")
    fun upload(@Part("refId") refId: RequestBody,
               @Part("title") title: RequestBody,
               @Part("sortOrder") sortOrder: RequestBody,
               @Part file: MultipartBody.Part): Call<ApiResult>

    @GET("/download")
    fun download(@Query("id") id: Int): Call<ResponseBody>
}
```
这大概是问题的关键，@Multipart的表单项都必须用@Part注解，必须是RequestBody类型；文件项注解方式与非文件表单项不同，
而且必须是MultipartBody.Part类型。

##  客户端代码

``` 
class FileService {

    private val okHttpClient = OkHttpClient()
            .newBuilder()
            .addInterceptor(headerJsonInterceptor)
            .addInterceptor(loggingInterceptor)
            .build()

    private val retrofit = Retrofit
            .Builder()
            .baseUrl(BASE_URL)
            .client(okHttpClient)
            .addConverterFactory(GsonConverterFactory.create())
            .build()

    private val fileApi = retrofit.create(FileApi::class.java)

    fun upload(): Int {
        val refId: Int = 9
        val title = "my file"
        val sortOrder = 0

        val refIdPart = RequestBody.create(MultipartBody.FORM, "$refId")
        val titlePart = RequestBody.create(MultipartBody.FORM, title)
        val sortOrderPart = RequestBody.create(MultipartBody.FORM, "$sortOrder")

        val file = File(uploadDir, "horse.ogg")
        val filebody = RequestBody.create(MediaType.parse("multipart/form-data"), file)
        val filePart = MultipartBody.Part.createFormData("file", file.name, filebody)

        val call = fileApi.upload(refIdPart, titlePart, sortOrderPart, filePart)
        val response = call.execute().body()

        return if (response.code() == ApiCode.OK) response.data().toInt() else -1
    }

    fun download(id: Int) {
        val call = fileApi.download(id)
        val response = call.execute().body()
        val instream = response.byteStream()
        val file = File(uploadDir, "download.ogg")
        val outstream = file.outputStream()
        file.outputStream().buffered().use {
            instream.copyTo(outstream)
        }
    }
}

```

不难根据Api写出客户端代码：

-   普通表单项：```val titlePart = RequestBody.create(MultipartBody.FORM, title)```
-   文件表单项：```val filebody = RequestBody.create(MediaType.parse("multipart/form-data"), file) ```
-   Multipart: ```val filePart = MultipartBody.Part.createFormData("file", file.name, filebody) ```

##  再说Json转换 

客户端与服务器之间的数据交换，如果情况复杂，就通过ApiResult来进行封装（服务端请求结果数据的封装），code为定义的状态码，
desc是状态描述，data为实际数据。如果情况简单，要么得到期望的数据，要么什么都没得到，则无须ApiResult封装。

```
data class ApiResult(private var code: Int = 0, private var desc: String = "", private var data: String = "") : Serializable {

    constructor(json: String) : this() {
        code = JsonParser().parse(json).obj["code"].asInt
        desc = JsonParser().parse(json).obj["desc"].asString
        data = JsonParser().parse(json).obj["data"].asString
    }

    fun code() = this.code
    fun desc() = this.desc
    fun data() = this.data

    fun <T> data(aClass: Class<T>): T? {
        if (code == ApiCode.ERROR) return null
        val gson = GsonBuilder()
                .registerTypeAdapter(DateTime::class.java, JodaGsonAdapter())
                .setLenient()
                .create()
        try {
            return gson.fromJson<T>(data, aClass)
        } catch (e: Exception) {
            println(e.stackTrace)
            return null
        }
    }

    fun <T> data(type: Type): T? {
        if (code == ApiCode.ERROR) return null
        val gson = GsonBuilder()
                .registerTypeAdapter(DateTime::class.java, JodaGsonAdapter())
                .setLenient()
                .create()
        try {
            return gson.fromJson<T>(data, type)
        } catch(e: Exception) {
            println(e.stackTrace)
            return null
        }
    }
}
```

其中data为String型.

-   如果是基本类型，或简单对象类型，或简单对象的列表类型，就直接赋值；
-   如果是Map类型，而且其中的元素是象类型，或者列表类型，则先要将元素转换为json，再放进map中，再将map转换为json，再赋值给ApiResult.data.
-   再将ApiResult用JsonResponse封装，实际是将JsonResponse封装的作何数据，都将转换为json:
``` 
call.transform.register<JsonResponse> { value ->
   TextContent(gson.toJson(value.data), ContentType.Application.Json)
}
```

>   原则是，在服务端对象据转换几次json，在客户端就要回转几次json，数据才能复原。与encode/decode类似。

Retrofit: 2.2.0

OkHttp: 3.6.0


参考：[https://futurestud.io/tutorials/retrofit-2-how-to-upload-files-to-server]https://futurestud.io/tutorials/retrofit-2-how-to-upload-files-to-server

