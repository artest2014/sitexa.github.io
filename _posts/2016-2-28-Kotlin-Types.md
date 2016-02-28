---
layout: post
title: Kotlin -- Types
category: 'technology'
---

              
## Numbers

    Type	Bit width
    Double	64
    Float	32
    Long	64
    Int	32
    Short	16
    Byte	8
    
## Representation

Note that boxing of numbers does not preserve identity:
    
    val a: Int = 10000
    print(a === a) // Prints 'true'
    val boxedA: Int? = a
    val anotherBoxedA: Int? = a
    print(boxedA === anotherBoxedA) // !!!Prints 'false'!!!

On the other hand, it preserves equality:
    
    val a: Int = 10000
    print(a == a) // Prints 'true'
    val boxedA: Int? = a
    val anotherBoxedA: Int? = a
    print(boxedA == anotherBoxedA) // Prints 'true'
    
##Explicit Conversions
    
    // Hypothetical code, does not actually compile:
    val a: Int? = 1 // A boxed Int (java.lang.Integer)
    val b: Long? = a // implicit conversion yields a boxed Long (java.lang.Long)
    print(a == b) // Surprise! This prints "false" as Long's equals() check for other part to be Long as well
    
    val b: Byte = 1 // OK, literals are checked statically
    val i: Int = b // ERROR
    
    val i: Int = b.toInt() // OK: explicitly widened
    
-   toByte(): Byte
-   toShort(): Short
-   toInt(): Int
-   toLong(): Long
-   toFloat(): Float
-   toDouble(): Double
-   toChar(): Char


##Operations

-   shl(bits) – signed shift left (Java’s <<)
-   shr(bits) – signed shift right (Java’s >>)
-   ushr(bits) – unsigned shift right (Java’s >>>)
-   and(bits) – bitwise and
-   or(bits) – bitwise or
-   xor(bits) – bitwise xor
-   inv() – bitwise inversion
    
##Characters
    
    fun check(c: Char) {
      if (c == 1) { // ERROR: incompatible types
        // ...
      }
    }
    
    un decimalDigitValue(c: Char): Int {
      if (c !in '0'..'9')
        throw IllegalArgumentException("Out of range")
      return c.toInt() - '0'.toInt() // Explicit conversions to numbers
    }
    
##Booleans : true or false
    
-   || – lazy disjunction
-   && – lazy conjunction
-   ! - negation    

##Arrays

    class Array<T> private constructor() {
      val size: Int
      fun get(index: Int): T
      fun set(index: Int, value: T): Unit
    
      fun iterator(): Iterator<T>
      // ...
    }
    
    // Creates an Array<String> with values ["0", "1", "4", "9", "16"]
    val asc = Array(5, { i -> (i * i).toString() })
    
    val x: IntArray = intArrayOf(1, 2, 3)
    x[0] = x[1] + x[2]
    
##Strings

    for (c in str) {
      println(c)
    }
    
    val s = "Hello, world!\n"
    
    val text = """
      for (c in "foo")
        print(c)
    """
    
##String Templates
    
    val i = 10
    val s = "i = $i" // evaluates to "i = 10"
    
    val s = "abc"
    val str = "$s.length is ${s.length}" // evaluates to "abc.length is 3"
    
    val price = """
    ${'$'}9.99
    """