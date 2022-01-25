---
layout:     post
title:      2021-12-08-c# delegates
subtitle:   Advanced topics on c#
date:       2021-12-08
author:     BY HY
header-img: img/post-bg-csharp-dotnet.png
catalog: true
tags:
    - c#
    - Advanced Topics
---
## What's a delegate?

A delegate is a type safe function pointer. The function must have matched return type, parameter list.

Both static and instance methods could have delegate.

## [Covariance and Contravariance 协变与逆变](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/covariance-contravariance/)


**Covariance** and **Contravariance** enable implicit reference conversion of array types, delegate types, and generic type arguments. Covariance preserves assignment compatibility and Contravariance reverse it.

```c#
// 赋值兼容性Assignment compatibility.
string str = "test";  
// 父类变量可以引用子类实例An object of a more derived type is assigned to an object of a less derived type.
object obj = str;  
  
// 协变Covariance.
IEnumerable<string> strings = new List<string>();  
// 父类变量数组可以引用子类实例数组An object that is instantiated with a more derived type argument
// is assigned to an object instantiated with a less derived type argument.
// Assignment compatibility is preserved.
IEnumerable<object> objects = strings;  
// 此操作不是类型安全type-safe的操作
object[] array = new String[10];  
// The following statement produces a run-time exception.  
// array[0] = 10;
  
// 逆变Contravariance.
// Assume that the following method is in the class:
// static void SetObject(object o) { }
Action<object> actObject = SetObject;  
// 子类实例泛型可以引用父类实例泛型。An object that is instantiated with a less derived type argument
// is assigned to an object instantiated with a more derived type argument.
// Assignment compatibility is reversed.
Action<string> actString = actObject;
// 如果泛型接口或委托的泛型参数被声明为协变或逆变，该泛型接口或委托则被称为“变体”。

//Delegates支持协变和逆变
//对方法组的协变和逆变支持允许将方法签名与委托类型相匹配Covariance and contravariance support for method groups allows for matching method //signatures with delegate types. This enables you to assign to delegates not only //methods that have matching signatures, but also methods that return more derived types //(covariance) or that accept parameters that have less derived types (contravariance) //than that specified by the delegate type.
static object GetObject() { return null; }  
static void SetObject(object obj) { }  
  
static string GetString() { return ""; }  
static void SetString(string str) { }  
  
static void Test()  
{  
    // Covariance. A delegate specifies a return type as object,  
    // but you can assign a method that returns a string.  
    Func<object> del = GetString;  
  
    // Contravariance. A delegate specifies a parameter type as string,  
    // but you can assign a method that takes an object.  
    Action<string> del2 = SetObject;  
}
```

## Three built-in generic delegates: Func, Action and Predicates

Use generic types to maximize code reuse, type safety and performance

```c#
//It allows 0, up to 16 inputs
public delegate TResult Func< in T1, in T2, ..., in T16, out TResult>(T1 arg1, T2 arg2, ..., T16 arg16);

// Action allows only void return type
public delegate void Action<in T>(T arg);

// Predicate allows only boolean return type
public delegate bool Predicate<in T>(T arg);
```

They can also be used with *anonymous methods, lambda expression, static extension methods*.

## [AsyncCallback in delegate](https://docs.microsoft.com/en-us/dotnet/api/system.asynccallback?view=net-6.0)

Sample

```c#
public delegate void AsyncCallback(IAsyncResult ar);
```



## Summary

A *delegate* is a reference type in C# that references a method that contains a particular parameter list and return type.

*Contravariance* means that a delegate can reference a method where a particular parameter definition is more derived the parameter counter contained within the delegated method.

*Covariance* means that the return type in the delegates definition can be less derived than the return type of the delegated method.
