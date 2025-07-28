---
title: "5 C# Features to Avoid Duplicate Code in Your Project"
date: 2025-07-26
image: /assets/images/5 Csharp Features to Avoid Duplicate Code in Your Project - The Good Engineers.png
header:
  teaser: 
  thumbnail: /assets/images/5 Csharp Features to Avoid Duplicate Code in Your Project - The Good Engineers.png
  og_image: /assets/images/5 Csharp Features to Avoid Duplicate Code in Your Project - The Good Engineers.png
categories:
  - csharp
tags:
  - c#
  - .NET
  - Code Quality
  - Software Engineering
excerpt: "Duplicate code is one of the biggest maintainability killers in any codebase. Here are 5 powerful C# features that help you write cleaner, reusable, and maintainable code."
redirect_from:
  - /csharp/10-csharp-features-to-avoid-duplicate-code/
---

![image](/assets/images/5 Csharp Features to Avoid Duplicate Code in Your Project - The Good Engineers.png)

I’ve reviewed thousands of lines of C# code over the years—from junior dev prototypes to enterprise-scale platforms.

You know what I see way too often?

**Duplicate code.**

Same validation logic in 4 places. Repeated try-catch blocks. Copy-paste service calls with slight variations.

It’s not always intentional. Sometimes it’s just lack of awareness. So today, I want to help you fix that.

Here are **5 powerful features in C#** that help you eliminate duplication, improve maintainability, and write more elegant, DRY code.
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


Use it where it improves clarity. But don’t over-optimize readability.
## 4. Delegates and Func<>
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

## 5. Base Classes and Abstract Classes
Classic OOP still works.

When you find yourself writing the same methods across services or controllers, extract a base class.
```
public abstract class ControllerBase
{
    protected void Log(string message) { ... }
}
```
Reusability is the foundation of clean architecture.

Just don’t go too deep with inheritance—prefer composition when it makes sense.


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








