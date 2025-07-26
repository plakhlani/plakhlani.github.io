---
title: "10 C# Features to Avoid Duplicate Code in Your Project"
date: 2025-07-26
image: /assets/images/10 Csharp Features to Avoid Duplicate Code in Your Project - The Good Engineers.png
header:
  teaser: 
  thumbnail: /assets/images/10 Csharp Features to Avoid Duplicate Code in Your Project - The Good Engineers.png
  og_image: /assets/images/10 Csharp Features to Avoid Duplicate Code in Your Project - The Good Engineers.png
categories:
  - csharp
tags:
  - c#
  - .NET
  - Code Quality
  - Software Engineering
excerpt: "Duplicate code is one of the biggest maintainability killers in any codebase. Here are 10 powerful C# features that help you write cleaner, reusable, and maintainable code."
---

![image](/assets/images/10 Csharp Features to Avoid Duplicate Code in Your Project - The Good Engineers.png)

I’ve reviewed thousands of lines of C# code over the years—from junior dev prototypes to enterprise-scale platforms.

You know what I see way too often?

**Duplicate code.**

Same validation logic in 4 places. Repeated try-catch blocks. Copy-paste service calls with slight variations.

It’s not always intentional. Sometimes it’s just lack of awareness. So today, I want to help you fix that.

Here are **10 powerful features in C#** that help you eliminate duplication, improve maintainability, and write more elegant, DRY code.
## 1. Extension Methods

Have you ever needed to check for null or trim a string in multiple places?

Instead of writing the same utility code everywhere, use **extension methods**.

```
public static class StringExtensions
{
    public static bool IsNullOrEmpty(this string value)
        => string.IsNullOrEmpty(value);
}
```
Now you can call "hello".IsNullOrEmpty() as if it’s part of the string class.

Use them to:

- Add behavior to types you don’t control
- Keep helpers scoped to a namespace
- Improve readability and reuse

But avoid abuse—don’t hide complex logic in obscure extensions.

## 2. Generics
If you’ve written two methods that differ only by type, you probably need generics.
```
public T FirstOrDefaultSafe<T>(IEnumerable<T> source)
{
    return source?.FirstOrDefault();
}
```
Generics let you abstract away type details. This prevents duplication across types and promotes reusable libraries.

Use generics for:
- Repository patterns
- Utility methods
- Common service responses

Good engineers abstract patterns. Great engineers abstract types too.

### 3. Attributes and Reflection
Imagine having 10 different model classes and needing to validate a property called Email.

Instead of repeating logic everywhere, use custom attributes and scan them with reflection.
```
[Required]
[EmailAddress]
public string Email { get; set; }
```
Frameworks like ASP.NET Core do this already with [DataAnnotation] attributes.

But you can write your own for:
- Custom validation
- Auditing
- Caching behavior

Define once. Apply everywhere.
## 4. Pattern Matching
Say goodbye to long chains of if-else or type checks.

With pattern matching, you can simplify conditionals and avoid repeating boilerplate.
```
if (obj is Customer c && c.IsActive)
{
    // use c directly
}
```
Switch expressions, type patterns, property patterns—they all help you write less code with more clarity.

Look into:
- `switch` expressions `(switch { ... })`
- Tuple patterns
- `when` clauses for condition matching

Cleaner branching = less repeated logic.

## 5. LINQ (Language Integrated Query)
Before LINQ, I used to write loops everywhere.

Now? I use `Where`, `Select`, `Any`, `All`, `GroupBy`, `Aggregate`.
```
var activeUsers = users.Where(u => u.IsActive).ToList();
```
With LINQ, you express your intent. No need to rewrite the same for loop logic in 10 places.

It reduces:
- Looping duplication
- Projection logic
- Filtering conditions

Bonus: chainable, readable, testable.
## 6. Expression-Bodied Members
For small methods and properties, skip the boilerplate.
```
public int Age => DateTime.Now.Year - BirthYear;
```
Or
```
public string FullName() => $"{FirstName} {LastName}";
```
Cleaner syntax = less code = less duplication.

Use it where it improves clarity. But don’t over-optimize readability.
## 7. Delegates and Func<>
Sometimes logic changes, but structure doesn’t.

Instead of duplicating entire methods, pass the changing logic as a delegate.
```
public void ProcessData(Func<string, string> transform)
{
    var raw = "input";
    var result = transform(raw);
    Console.WriteLine(result);
}
```
Now you can inject logic like:
- `s => s.ToUpper()`
- `s => new string(s.Reverse().ToArray())`

Delegates keep structure constant and logic flexible.

## 8. Base Classes and Interfaces
Classic OOP still works.

When you find yourself writing the same methods across services or controllers, extract a base class or interface.
```
public interface ILoggable
{
    void Log(string message);
}
```
Or a base class:
```
public abstract class ControllerBase
{
    protected void Log(string message) { ... }
}
```
Reusability is the foundation of clean architecture.

Just don’t go too deep with inheritance—prefer composition when it makes sense.

## 9. Record Types and Object Initializers
When working with data objects, avoid writing repetitive constructors or mapping logic.

With record types (introduced in C# 9), you can create immutable models with minimal code:
```
public record User(string Name, string Email);
```
Pair with object initializers for quick, readable object construction:
```
var user = new User { Name = "Alex", Email = "alex@example.com" };
```
Less boilerplate = fewer places to introduce inconsistency.

## 10. Global Using Directives (C# 10+)
Tired of repeating using System; and using MyApp.Common; in every file?

Define them once with global usings:
```
// GlobalUsings.cs
global using System;
global using MyApp.Common;
```
Now your entire project gets access—without duplicate using statements in every file.

A small change, but it adds up quickly in large projects.

## Final Thoughts
Duplicate code is more than just a code smell—it’s a future maintenance nightmare.

When the same logic exists in 5 places:
- It’s harder to change
- Easy to break
- Painful to test

The C# language gives you powerful tools to keep your code DRY. But it’s on you to apply them with care.

So next time you catch yourself copy-pasting—pause.

Ask: Can I extract this into a method? An extension? A generic helper?

Clean code is more than writing fewer lines.

It’s about building systems that grow with your team—and don’t collapse under their own weight.

---

Want more posts like this on software engineering, .NET, C#, Web Development and SaaS? Subscribe for weekly insights.








