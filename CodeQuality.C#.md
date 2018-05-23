# C# Coding Standards Guidance

## Table of Contents

<!-- TOC -->

1. [C# Coding Standards Guidance](#c-coding-standards-guidance)
    1. [Table of Contents](#table-of-contents)
    2. [Introduction](#introduction)
    3. [Design & Maintainability](#design--maintainability)
        1. [General Design](#general-design)
        2. [Classes & Interfaces](#classes--interfaces)
        3. [Methods](#methods)
        4. [Members](#members)
        5. [Error Handling](#error-handling)
        6. [File Organisation](#file-organisation)
        7. [](#)

<!-- /TOC -->

## Introduction

As part of a larger team of developers delivering software to external clients it is important that each team member produces code that is consistently formatted and documented. This document is therefore intended to provide an overview of coding standards that should be applied to any software solution that is produced.

By observing the conventions lad out herein, it is expected that any developer should be able to look at any other developers' code and quickly orient themselves with a minimum of delay.

The standards laid out in this document specifically apply to C# code, however many of the concepts can be applied to other software languages

## Design & Maintainability

### General Design

* Respect the principles of [SOLID](https://en.wikipedia.org/wiki/SOLID) design

* Use type aliases such as `string` over `String` and `int` over `Int32`

### Classes & Interfaces

* Classes and Interfaces should have a single purpose. Complex objects should be split into smaller, logical objects

* Where similar functionality is shared between multiple classes consider using an abstract base class and inheritance

* Where inheriting from a base class, it should always be possible to treat the derived object as if it were an instance of the base class

* Where appropriate, use interfaces to decouple classes from each other

* Do not hide members inherited from a base class with the `new` keyword

* A base or abstract class should never refer to or have dependencies upon any of its derived classes

* Avoid exposing the objects an object depends on

* When referencing members of a class from within, ensure that you always use the `this` keyword

* When referencing members of a base class, ensure that you use the `base` keyword

* Avoid the creation of partial classes spread across multiple files. This is generally an indication that the class is too complex and should be broken into smaller, more focused, classes

### Methods

* As with classes, a method should have a single purpose and complex methods should be split into smaller, logical chunks to allow for code reuse and improved readability

* Evaluate the result of a LINQ expression before returning it

* Favour returning an interface or construct over concrete classes where available:

```CSharp
public IEnumerable<TType> GetObjects();
```

### Members

* Allow properties to be set in any order

* Do not use mutually exclusive properties:

```CSharp
public bool HasData;
public bool HasNoData;
```

* Do not expose stateful objects through static members

* Properties and arguments representing strings or collections should never be null. Instead they should be initialised according to their type:

```CSharp
string name = string.Empty;
List<string> names = new List<string>();
```

* Where no additional logic is required, automatic properties should be used for public members

```CSharp
public string Name { get; set; }
```

### Error Handling

* Check that valid parameters have been passed into a method as early as possible and throw an appropriate error message when this is not the case:

```CSharp
if (string.IsNullOrWhiteSpace(username))
{
    throw new ArgumentNullException(nameof(username));
}
```

* Throw exceptions which can be caught further up the call stack rather than returning status values which could be incorrectly interpreted as a valid result

* Provide rich and meaningful message text when throwing exceptions so as to provide as much information as possible for debugging

* Where possible, avoid swallowing exceptions:

```CSharp
try
{
    // Complex operation
}
catch
{
}
```

* Where possible, record errors and debug information to theWindows event log or another, appropriate, tool to aid in debugging

### File Organisation

* Source files should, generally, contain only a single type

* Source files should be named according to the type they contain

### 