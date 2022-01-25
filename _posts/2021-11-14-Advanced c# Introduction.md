---
layout:     post
title:      2021-11-14-c# introduction
subtitle:   Advanced topics on c#
date:       2021-11-14
author:     BY Elon
header-img: img/post-bg-csharp-main.png
catalog: true
tags:
    - c#
    - Advanced Topics
---
# Introduction - Advanced C#

## Draft Version 1.0

```c#
// To build a school HR admin system
// First build an interface
public interface IEmployee
{
    int Id { get; set; }
    string FirstName { get; set; }
    string LastName { get; set; }
    decimal Salary { get; set; }
}
```

Build an base class

```c#
public class EmployeeBase : IEmployee
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public virtual decimal Salary { get; set; }
}
```

Build several child classes of EmployeeBase: Teacher, HeadOfDepartment, DeputyHeadMaster, HeadMaster.

```c#
public class Teacher : EmployeeBase
{
    public override decimal Salary { get => base.Salary + (base.Salary * 0.02m); }
}

public class HeadOfDepartment : EmployeeBase
{
    public override decimal Salary { get => base.Salary + (base.Salary * 0.03m); }
}

public class DeputyHeadMaster : EmployeeBase
{
    public override decimal Salary { get => base.Salary + (base.Salary * 0.04m); }
}

public class HeadMaster : EmployeeBase
{
    public override decimal Salary { get => base.Salary + (base.Salary * 0.05m); }
}
```

Then we will seed data in the program.

```c#
public static void SeedData(List<IEmployee> employees)
{
    IEmployee teacher1 = new Teacher
    {
        Id = 1, 
        FirstName = "Test",
        LastName = "Just",
        Salary = 40000
    };
    IEmployee teacher2 = new Teacher
    {
        Id = 2, 
        FirstName = "Test2",
        LastName = "Just",
        Salary = 40000
    };
    IEmployee headOfDepartment = new HeadOfDepartment
    {
        Id = 3, 
        FirstName = "Test3",
        LastName = "Just",
        Salary = 40000
    }
    //...
}
```

(Refactor Phase1), However, we could have a better to way by using **Factory Pattern** to seed data,

```c#
public static class EmployeeFactory
{
    public static IEmployee GetEmployeeInstance(
        EmployeeType employeeType,
        int id,
        string firstName,
        string lastName,
        decimal salary)
    {
        IEmployee employee = null;
        switch (employeeType)
        {
            case EmployeeType.Teacher:
                employee = new Teacher
                {
                    Id = id,
                    FirstName = firstName,
                    LastName = lastName,
                    Salary = salary
                };
                break;
            case EmployeeType.HeadOfDepartment:
                employee = ...
                break;
            case EmployeeType.DeputyHeadMaster:
                employee = ...
                break;
            case EmployeeType.HeadMaster:
                employee = ...
                break;
            default:
                break;
        }
        
        return employee;
    }
}
```

Further, (Phase 2), we could use **generic** to make Factory Pattern more easier

```c#
public static class FactoryPattern<K, T> where T:class, K, new()
{
    public static K GetInstance()
    {
        K objk;
        objk = new T();
        return objk;
    }
}

public static class EmployeeFactory
{
    public static IEmployee GetEmployeeInstance(
        EmployeeType employeeType,
        int id,
        string firstName,
        string lastName,
        decimal salary)
    {
        IEmployee employee = null;
        switch (employeeType)
        {
            case EmployeeType.Teacher:
                employee = FactoryPattern<IEmployee, Teacher>.GetInstance();
                break;
            case EmployeeType.HeadOfDepartment:
                employee = FactoryPattern<IEmployee, HeadOfDepartment>.GetInstance();
                break;
            case EmployeeType.DeputyHeadMaster:
                employee = FactoryPattern<IEmployee, DeputyHeadMaster>.GetInstance();
                break;
            case EmployeeType.HeadMaster:
                employee = FactoryPattern<IEmployee, HeadMaster>.GetInstance();
                break;
            default:
                break;
        }
        if (employee != null)
        {
            employee.Id = id;
            employee.FirstName = firstName;
            employee.LastName = lastName;
            employee.Salary = salary;
        }
        else
        {
            throw new NullReferenceException();
        }
        return employee;
    }
}
```

In our program.cs, we could use **LINQ** to make easier for-loop,

```c#
SeedData(employees);

//foreach(IEmployee employee in employees)
//{
//    totalSalaries += employee.Salary;
//}
//Console.WriteLine($"Total Annual Salaries (including bonus): {totalSalaries}");
totalSalaries = employees.Sum(x => x.Salary);
Console.WriteLine($"Total Annual Salaries (including bonus): {totalSalaries}");
```

## Generics

1, 

2, [Constraints on type parameters](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/constraints-on-type-parameters)

- Constraints inform the compiler about the capabilities a type argument must have. Without any constraints, the type argument could be any type.

- Constraints are specified by using the `where` contextual keyword.

- lists of contraint types:

  | -                             | -                                                            |
  | ----------------------------- | ------------------------------------------------------------ |
  | `where T : struct`            | The type parameter must be a non-nullable value type. The `struct` constraint implies the `new()`constraint and can't be combined with new() and also can't combined with `unmanaged`. |
  | `where T : class`             | The type parameter must be a reference type. In c# 8.0 or above, T must be a non-nullable reference type. |
  | `where T : class?`            | The type argument must be a reference type, either nullable or non-nullable. This constraint applies also to any class, interface, delegate, or array type. |
  | `where T : notnull`           | The type argument must be a non-nullable type. Eiter reference type or value type. |
  | `where T : default`           | :question:This constraint resolves the ambiguity when you need to specify an unconstrained type parameter when you override a method or provide an explicit interface implementation. |
  | `where T : unmanaged`         | - `sbyte, byte, short, ushort, int, uint, long, ulong, char, float, decimal, double, or bool`<br />- any `enum` type<br />- any `pointer` type<br />- any user-defined `struct` with unmanaged type<br />* primitive types |
  | `where T : new()`             | The type argument must have a public parameterless constructor. When used together with other constraints, the `new()` constraint must be specified last. |
  | `where T : <base class name>` | The type argument must be or derive from the specified base class. |
  | `where T : <interface name>`  | The type argument must be or implement the specified interface. Multiple interface constraints can be specified. |
  | `where T : U`                 | The type argument supplied for `T` must be or derive from the argument supplied for `U`. |

* Constraints specify the capabilities and expectations of a type parameter. Declaring those constraints means you can use the operations and method calls of the constraining type.
* When applying the `where T : class` constraint, avoid the `==` and `!=` operators on the type parameter because these operators will test for reference identity only, not for value equality.  The recommended way is to also apply the `where T : IEquatable<T>` or `where T : IComparable<T>` constraint and implement the interface in any class that will be used to construct the generic class.

## Job1: Implement a linked list in c# using Generics



Job2: 

## Summary
* What makes a concept in programming a more advanced concept? The more abstract the concept the more difficult the concept is to understand for most people. Gaining an understanding of the more abstract advanced concepts can be applied to achieve better code reuse, cleaner code, extensibility, flexibility of design, ease of code maintenance, separation of concerns, the enablement of effective unit testing and the provision for overall better performance and efficiency of our applications.
* The more advanced concepts are applied frequently in the various .Net project frameworks like ASP .NET MVC, Web API and Xamarin. Understanding these advanced concepts will also be an advantage to game developers that create games using the Unity Game Engine.
* Some of the advanced concepts that will be explored in detail in this series will be : **Delegates**, **Events**, **Generics**, **Extensions Methods**, **Lambda Expressions**, Linq, **Asynchronous Programming with async/await, attributes, Reflection and more... 