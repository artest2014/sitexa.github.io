---
layout: post
title: Kotlin -- Idioms
category: 'technology'
---

              
##  com.sitexa.syntax.basic.Idioms.kt

    package com.sitexa.syntax.basic
    
    import java.io.File
    import java.nio.file.Files
    import java.nio.file.Paths
    
    fun main(args: Array<String>) {
    
        val map = mapOf("a" to 1, "b" to 2, "c" to 3, "d" to 4);
    
        for ((k, v) in map) {
            println("$k -> $v");
        }
    
        val list = listOf("a", "b", "c", "d");
        for (l in list) {
            println(l);
        }
    
        val files = File("/").listFiles();
        println("files count:" + files?.size);
    
        println("Color:" + transform("Green"));
    
        println("IntArray:")
        val iar = arrayOfMinusOnes(5);
        for (i in iar) {
            println(i);
        }
    
        println("call turtle")
        turtle()
    
        println("java7try")
        java7try();
    }
    
    fun transform(color: String): Int {
        return when (color) {
            "Red" -> 0;
            "Green" -> 1;
            "Blue" -> 2;
            else -> throw IllegalArgumentException("Invalid coloe name");
        }
    }
    
    fun transform2(color: String): Int = when (color) {
        "Red" -> 0;
        "Green" -> 1;
        "Blue" -> 2;
        else -> throw IllegalArgumentException("Invalid coloe name");
    }
    
    fun arrayOfMinusOnes(size: Int): IntArray {
        return IntArray(size).apply { fill(-1) }
    }
    
    fun theAnswer() = 42;
    
    class Turtle {
        fun penDown() {
            println("penDown")
        }
    
        fun penUp() {
            println("penUp")
        }
    
        fun turn(degrees: Double) {
            println(degrees)
        }
    
        fun forward(pixels: Double) {
            println(pixels)
        }
    }
    
    fun turtle() {
        val myTurtle = Turtle();
        with(myTurtle) {
            penDown()
            for (i in 1..4) {
                forward(100.0)
                turn(90.0)
            }
            penUp()
        }
    }
    
    fun java7try() {
        val stream = Files.newInputStream(Paths.get("/tmp/adobegc.log"))
        stream.buffered().reader().use { reader ->
            println(reader.readText())
        }
    }
    
    