---
layout: post
title: Kovenant - Promise for Kotlin
category: 'technology'
---

The easy asynchronous library for Kotlin. With extensions for Android, RxJava, JavaFX and much more.

Developed with the following goals in mind:

-   Easy to use: Function above anything else
-   Runtime agnostic: API layer must be pure Kotlin
-   Memory efficient: trying to reduce the overhead as much as possible
-   Non blocking: besides being thread safe everything should be non blocking (JVM)
-   Dependency free: when not counting kotlin std

#  Kovenant Core Usage

##  Task

The easiest way to create a Promise is by using task, e.g.

```
val promise = task { foo() }
```

This will execute function foo() asynchronously and immediately returns a Promise<V, Exception> where V is the inferred return type of foo(). If foo() completes successful the Promise is resolved as successful. Any Exception from foo() is considered a failure.

##  Deferred

With a Deferred<V,E> you can take matters in your own hand.

```
fun foo() {
    val deferred = deferred<String,Exception>()
    handlePromise(deferred.promise)

    deferred.resolve("Hello World")
//    deferred.reject(Exception("Hello exceptional World"))
}
fun handlePromise(promise: Promise<String, Exception>) {
    promise success {
        msg -> println(msg)
    }
    promise fail {
        e -> println(e)
    }
}
```

##  Cancelable Deferred

By default the promise returned by a Deferred is not a CancelablePromise. Simply because there is no way to tell the owner of the Promise that a cancel has been requested. If we however provide a callback to the deferred function we are able to cancel. What cancelling means is of course up to the one owning the Deferred.

```
val deferred = deferred<Int, String> {
    //callback method to receive notification
    //when cancel is requested
    println("I'm cancelled by $it")
}

//Convenience method for trying to cancel promises
Kovenant.cancel(deferred.promise, "test method")
```

##  Callbacks

A Promise<V, E> allows you to add 3 types of callbacks:

-   success of type (V) -> Unit
-   fail of type (E) -> Unit
-   always of type () -> Unit

```
val promise = task {
    //mimicking those long running operations with:
    1 + 1
}

promise success {
    //called on succesfull completion of the promise
    println("result: $it")
}

promise fail {
    //called when an exceptions has occurred
    println("that's weird ${it.message}")
}

promise always {
    //no matter what result we get, this is always called once.
}
```

##  Chaining

All callback registering functions return this Promise, thus previous example can be written without those intermediate variables

```
task {
    //some (long running) operation, or just:
    1 + 1
} success {
    //called when no exceptions have occurred
    println("result: $it")
} fail {
    //called when an exceptions has occurred
    println("that's weird ${it.message}")
} always {
    //no matter what result we get, this is always called once.
}
```

##  DispatcherContext

By default the callbacks are executed on the callback DispatcherContext that is associated with this Promise. But you can also provide your own DispatcherContext for a specific callback.

```
val dispatcherContext = //...

task {
    foo()
}.success(dispatcherContext) {
    bar()
}
```

##  Multiple Success stories

You don't have to limit yourself to registering just one callback. You can add multiple success, fail and always actions to one single promise.

```
task {
    1 + 1
} success {
    println("1")
} success {
    println("2")
} success {
    println("3")
}
```

##  Execution order

```
val firstRef = AtomicReference<String>()
val secondRef = AtomicReference<String>()

val first = task { "hello" } success {
    firstRef.set(it)
}
val second = task { "world" } success {
    secondRef.set(it)
}

all (first, second) success {
    println("${firstRef.get()} ${secondRef.get()}")
}
```

##  Then

```
task {
    fib(20)
} then {
    "fib(20) = $it, and fib(21) = (${fib(21)})"
} success {
    println(it)
}
```

##  ThenApply

```
task {
    fib(20)
} thenApply {
    "fib(20) = $this, and fib(21) = (${fib(21)})"
} success {
    println(it)
}
```

##  Get

```
val fib20 : Int = task { fib(20) }.get()
```

##  isDone


##  Lazy Promise

```
val expensiveResource by lazyPromise {
    println("init promise")
    ExpensiveResource()
}

fun main(args: Array<String>) {
    println("start program")

    expensiveResource thenApply {
        "Got [$value]"
    } success {
        println(it)
    }
}


class ExpensiveResource {
    val value :String = "result"
}
```

##  Of

```
// Success promise with inferred value type
// and Exception as fail type
Promise.of(13)

// Failed promise with explicit types
Promise.ofFail<String, Int>(13)

// Successful promise with explicit types
Promise.ofSuccess<String, Int>("thirteen")
```

##  All

```
val promises = Array(10) { n ->
    task {
        Pair(n, fib(n))
    }
}

all(*promises) success {
    it forEach { pair -> println("fib(${pair.first}) = ${pair.second}") }
} always {
    println("All ${promises.size()} promises are done.")
}
```

##  Any

```
val promises = Array(10) { n ->
    task {
        while(!Thread.currentThread().isInterrupted()) {
            val luckyNumber = Random(System.currentTimeMillis() * n).nextInt(100)
            if (luckyNumber == 7) break
        }
        "Promise number $n won!"
    }
}

any (*promises) success { msg ->
    println(msg)
    println()

    promises forEachIndexed { n, p ->
        p.fail { println("promise[$n] was canceled") }
        p.success { println("promise[$n] finished") }
    }
}
```

##  Cancel


##  Void


##  unwrap

```
val nested = Promise.of(Promise.of(42))
val promise = nested.unwrap()
promise success {
    println(it)
}
```

##  withContext

```
val p = Promise.of(42).withContext(Kovenant.context)
```

#   Example

```
class SunService {
fun getSunInfo(lat: Double, lon: Double): Promise<SunInfo, Exception> = task {
    val url = "http://api.sunrise-sunset.org/json?lat=$lat&lng=$lon&formatted=0"
    val (request, response, result) = url.httpGet().responseString()
    val jsonStr = String(response.data, Charset.forName("UTF-8"))
    val json = JsonParser().parse(jsonStr).obj
    val sunrise = json["results"]["sunrise"].string
    val sunset = json["results"]["sunset"].string
    val sunriseTime = DateTime.parse(sunrise)
    val sunsetTime = DateTime.parse(sunset)
    val formatter = DateTimeFormat.forPattern("HH:mm:ss").withZone(DateTimeZone.forID("Asia/Chongqing"))
    SunInfo(formatter.print(sunriseTime), formatter.print(sunsetTime))
  }
}

class WeatherService {
fun getTemperature(lat: Double, lon: Double): Promise<Double, Exception> = task {
    val url = "http://api.openweathermap.org/data/2.5/weather?lat=$lat&lon=$lon&appid=d06f9fa75ebe72262aa71dc6c1dcd118&units=metric"
    val (request, response, result) = url.httpGet().responseString()
    val jsonStr = String(response.data, Charset.forName("UTF-8"))
    val json = JsonParser().parse(jsonStr).obj
    json["main"]["temp"].double
  }
}

router.get("/api/data").handler { ctx ->
    val lat = 28.1791667
    val lng = 113.1136111
    val sunInfoP = sunService.getSunInfo(lat, lng)
    val temperatureP = weatherService.getTemperature(lat, lng)
    val sunWeatherInfoP = sunInfoP.bind { sunInfo ->
        temperatureP.map { temp -> SunWeatherInfo(sunInfo, temp) }
    }
    sunWeatherInfoP.success { info ->
        val json = jsonMapper.writeValueAsString(info)
        val response = ctx.response()
        response.end(json)
    }
}

```




