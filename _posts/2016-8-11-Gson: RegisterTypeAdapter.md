---
layout: post
title: Gson - RegisterTypeAdapter
category: 'technology'
---

Gson is a Java library that can be used to convert Java Objects into their JSON representation. It can also be used to convert a JSON string to an equivalent Java object. Gson can work with arbitrary Java objects including pre-existing objects that you do not have source-code of.

##  DateTypeConverter

Json Data:

```
{"memberId":"64","memberName":"Kotlin","gender":"1","birthDate":315504000000,"mobile":"13311888009","email":"pxn4@qq.com","registerDate":1470743343000}
```

```birthDate```,```registerDate``` are Date in Long type. When convert with default Date Adapter, or set date format like
```val gson: Gson = GsonBuilder().setDateFormat("yyyy-MM-dd HH:mm:ss").create()```  These methods cannot convert Long type Date.
We must define a custom Date Adapter to treat the situation.

```
class DateTypeConverter : JsonSerializer<Date>, JsonDeserializer<Date> {
    override fun serialize(src: Date, srcType: Type, context: JsonSerializationContext): JsonElement {
        return JsonPrimitive(src.toString())
    }

    @Throws(JsonParseException::class)
    override fun deserialize(json: JsonElement, type: Type, context: JsonDeserializationContext): Date {
        try {
            return Date(json.asLong)
        } catch (e: IllegalArgumentException) {
            val date = context.deserialize<Date>(json, Date::class.java)
            return date
        }

    }
}

fun convert(){
    val json = """{"memberId":"64","memberName":"Kotlin","gender":"1","birthDate":315504000000,"mobile":"13311888009","email":"pxn4@qq.com","registerDate":1470743343000}"""
    val adapter = DateTypeConverter()
    val gson = GsonBuilder().registerTypeAdapter(Date::class.java, adapter).create()

    val m = gson.fromJson(json,Member::class.java)
    println(m)
}

result:

Member(memberId=64, memberName=Kotlin, gender=1, birthDate=Tue Jan 01 00:00:00 CST 1980, mobile=13311888009, email=pxn4@qq.com,registerDate=Tue Aug 09 19:49:03 CST 2016}

```

As you see, use which method depends on the data format, if date in json like '1990-01-01 20:10:20', use setDateFormat(),
if date in json is Long type like 315504000000, use custom one .

