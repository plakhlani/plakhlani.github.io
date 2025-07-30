---
title: "How to Use params with Collections in C# 13"
date: 2025-07-30
image: /assets/images/params with collections-The Good Engineers.png
header:
  teaser: 
  thumbnail: /assets/images/params with collections-The Good Engineers.png
  og_image: /assets/images/params with collections-The Good Engineers.png
categories:
  - csharp
tags:
  - csharp
  - .NET
  - Code Quality
  - Software Engineering
excerpt: "C# 13 finally lets `params` parameters accept any compatible collection type. Learn how this change makes your APIs clearer, faster, and more flexible."
redirect_from:
  - /csharp/10-csharp-features-to-avoid-duplicate-code/
---

![image](/assets/images/params with collections-The Good Engineers.png)

I remember the days when `params` in C# could only be arrays. Every method that needed flexibility had to accept `params T[]`, and every call packed arguments into an array—allocating on the heap.

That’s all changed in C# 13.

Now, `params` can target any collection type supported by collection expressions, `Span<T>`, `ReadOnlySpan<T>`, `IEnumerable<T>`, and more. It’s a quiet change, but it opens up clarity, flexibility, and performance benefits.

## What’s Changed with `params` in C# 13
Before, `params` meant one thing: an array. With C# 13, you can write:

```csharp
static void DoWork(params ReadOnlySpan<int> numbers) { /*...*/ }
DoWork(1, 2, 3);
```
or
```csharp
static void LogMessages(params IEnumerable<string> messages) { /*...*/ }
LogMessages("start", "process", "done");
```
That means you can now:
- Accept `Span<T>` or `ReadOnlySpan<T>` via params
- Use `IEnumerable<T>`, `IReadOnlyList<T>`, `ICollection<T>`, etc.
- Let the compiler generate the collection from a literal or inline value

## Why It Matters?
### 1. Zero-Allocation Performance
- `params` `Span<T>` lets the compiler allocate data on the stack, not the heap—no GC pressure.
- Compared to `params T[]`, it’s much faster and leaner.

### 2. Sharper API Intent
- If a method takes params ReadOnlySpan<T>, callers know it won’t modify the data.
- params IEnumerable<T> signals read-only and allows many input types—including LINQ results.

### 3. Cleaner Overloads
You can define overloads and rely on the compiler to pick the most efficient option:
```csharp
static void WriteNumbers(params ReadOnlySpan<int> nums) { … }
static void WriteNumbers(params IEnumerable<int> nums) { … }
```
Passing literal values or arrays picks the Span overload. Passing a `List<T>` uses the IEnumerable overload. No guessing needed.

## Examples in Action

### Example: Summing Integers with params Span<int>
```csharp
static int Sum(params ReadOnlySpan<int> values)
{
    int total = 0;
    foreach (var v in values)
        total += v;
    return total;
}

// Usage:
int result = Sum(1, 2, 3, 4, 5);
```
No array is allocated. All values are on the stack.

### Example: Logging Strings with `params IEnumerable<string>`
```csharp
static void Log(params IEnumerable<string> messages)
{
    foreach (var m in messages)
        Console.WriteLine(m);
}

// Works with:
Log("a", "b", "c");
Log(new[] { "x", "y" });
Log(myList.Where(m => m != null));
```
Handles arrays, LINQ results, lists—any IEnumerable seamlessly.

## When to Use Which `params` Type?

| Method Signature                          | Best For                                | Allocation Behavior               |
| ----------------------------------------- | --------------------------------------- | --------------------------------- |
| `params ReadOnlySpan<T>`                  | Performance‑critical, small items       | Stack‑alloc, zero heap allocation |
| `params Span<T>`                          | When mutability is needed inside method | Stack or heap based on size       |
| `params IEnumerable<T>` / ReadOnlyList<T> | General purpose flex‑API                | Synthesized collection if needed  |

## Things to Keep in Mind
### Overload Ambiguity
Don’t mix `params T[]` and `params Span<T>` without care. Compiler resolves overloads based on types. Carefully design overloads to avoid confusion.

### Invocation Rules
- Only one params parameter per method, and it must be last.
- You can pass a collection directly:
 - DoWork(new[] {1, 2, 3})
 - Or value list: DoWork(1, 2, 3)

### Performance Trade-offs
- Use Span<T> when you want maximum speed and no allocations.
- Use IEnumerable<T> for flexibility—but it may allocate internally if values come from value list.

## Why Sharp Engineers Should Care
- Cleaner API: Less boilerplate, clearer intent.
- Better performance: You avoid unnecessary memory allocation.
- More flexibility: Accept input in many forms, without multiple overloads.
This feature builds on the C# 12 collection expressions groundwork and brings it forward into APIs. It’s part of a bigger evolution toward expressive and efficient code.

## Final Thoughts
C# 13’s enhanced params collections bring a subtle—but meaningful—step forward. If you're writing performance-sensitive utilities or designing APIs for clarity, this feature gives you both.

Here’s how to get started:

- Use params ReadOnlySpan<T> where performance matters.
- Opt for params IEnumerable<T> when you want flexibility.
- Add overloads thoughtfully to guide the compiler toward the best match.
- Compile against .NET 9+ and enable C# 13 preview if needed.

This is a feature that’s particularly valuable if you care about clean APIs and optimized performance—both traits of seasoned engineers. If you’d like a companion blog post or code examples to practice with, just say the word!

---

Want more posts like this on software engineering, .NET, C#, Web Development and SaaS? Subscribe for weekly insights.
