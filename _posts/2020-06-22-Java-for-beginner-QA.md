---
layout:     post
title:      Java Tutorials - Q & A
subtitle:   2020-06-22-Top Interview Questions and resources for Java
date:       2020-06-22
author:     Elon
header-img: img/post-bg-coffee.jpg
catalog: true
tags:
    - Java
---

## 1, Java for beginner Video
### Separted videos
https://marcus-biel.com/java-beginner-course/
### Whole Video
https://www.youtube.com/watch?v=grEKMHGYyns

## 2, Special Topics
### 2.1, static vs. dynamic typing, compiled vs interpreted
https://hackernoon.com/i-finally-understand-static-vs-dynamic-typing-and-you-will-too-ad0c2bd0acc7

### 2.2, Compile-Error vs. Runtime Error
Compile time error is any type of error that prevent a java program compile like a syntax error, a class not found, a bad file name for the defined class, a possible loss of precision when you are mixing different java data types and so on.
 
A runtime error means an error which happens, while the program is running. To deal with this kind of errors java define Exceptions. Exceptions are objects represents an abnormal condition in the flow of the program. It can be either checked or unchecked.

### 2.3, Parameters can be passed by value or by reference.
https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value

All object references in Java are passed by value. This means that a copy of the value will be passed to a method. But the trick is that passing a copy of the value also changes the real value of the object. 
 
The reason is that Java object variables are simply references that point to real objects in the memory heap. Therefore, even though Java passes parameters to methods by value, if the variable points to an object reference, the real object will also be changed.

- Passing Object References - By Value
- Passing primitive types - By Value
- Passing immutable object reference like String
The JDK contains many immutable classes. Examples include the wrapper types Integer, Double, Float, Long, Boolean, BigDecimal, and of course the very well known String class.
 
 note that we’re not changing an attribute of the String class; instead, we’re simply assigning a new String value to it. In this case, the “Homer” value will be passed to name in the changeToHomer method. The String “Homer” will be eligible to be garbage collected as soon as the changeToHomer method completes execution. 
- Passing mutable object reference like StringBuilder


Java works exactly like C. You can assign a pointer, pass the pointer to a method, follow the pointer in the method and change the data that was pointed to. However, you cannot change where that pointer points.

In C++, Ada, Pascal and other languages that support pass-by-reference, you can actually change the variable that was passed.

### 2.4 Method Overloading vs overriding
函数重载与函数覆写
When a class has two or more methods by the same name but different parameters, it is known as method overloading. It is different from overriding. In overriding, a method has the same method name, type, number of parameters, etc.

### 2.5 Java Methods
https://www.tutorialspoint.com/java/java_methods.htm

### 2.6 Checked vs unchecked exception
It is saying that either the exception is checked at compile time or not. Under Error and RuntimeException classes are unchecked exceptions, like NullPointerException, ArithmeticException. Everything else under **Throwable** is checked exception.


## Head First To Design Pattern

### 2.7 Strategy design pattern vs Factory Design pattern

### 2.8 multi-thread safe - synchronized/volatile vs. static inner class vs. enum static class

### 2.9 interface vs. abstract class

### 3.0 adapter design pattern

### 3.1 decorator design pattern