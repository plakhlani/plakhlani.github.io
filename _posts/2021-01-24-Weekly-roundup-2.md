---
title: "Experimentor Weekly Journal - 02"
date: 2021-01-24
image:
header:
teaser:
thumbnail:
og_image:
categories:
- Weekly
tags:
- Weekly
excerpt: "My weekly journal 02 - Migrating ASP.NET Boilerplate from 4.3 to 5.0, read a book, health is wealth and more"
---

My weekly journal is series of blog posts where I share stories about my professional and personal work. This is my weekly Journal 02, Jan 24, 2021, and in this post, I am going to share with you about:

1. Migrating ASP.NET Boilerplate from 4.3 (.net core 2.2) to 5.0 (.net core 3.0).
2. Migrating from AWS DynamoDb to PostgreSQL.
3. File sharing is not a simple problem to solve.
4. I read [Platform: The Art and science of personal branding](https://www.goodreads.com/book/show/40983156-platform)
5. Health is wealth.

### Migrating ASP.NET Boilerplate from 4.3 (.Net Core 2.2) to 5.0 (.Net Core 3.0).

[ASP.NET Boilerplate](https://aspnetboilerplate.com/) is an open-source web application development starter template. One of our existing client at [Facile Technolab](https://www.faciletechnolab.com) is using [ASP.NET Boilerplate](https://aspnetboilerplate.com/) 4.3 (.Net Core 2.2) and wanted to migrate to [ASP.NET Boilerplate](https://aspnetboilerplate.com/) 5.0 (.Net Core 3.0).

There are some challenges that you have to face as:
1. [There are so many breaking changes](https://docs.microsoft.com/en-us/dotnet/core/compatibility/3.0) while switching to ASP.NET core 3.0
2. Due to [Entity Framework Core 3.0 breaking changes](https://docs.microsoft.com/en-us/ef/core/what-is-new/ef-core-3.x/breaking-changes), we have to rewrite some of the data access code
3. Additionally, there are changes in Abp specific packages.

We took the approach of generating a starter template from [ASP.NET Boilerplate](https://aspnetboilerplate.com/) version 5.0 from the [Module Zero Core Template](https://github.com/aspnetboilerplate/module-zero-core-template) github.com project and renamed it according to our project name.

Migrated all the .csproj file in the project to replace Package References and Framework References

And finally updated startup.cs of MVC project as the client was using ASP.NET MVC with jQuery version.

Lots of testing to ensure everything works. Obviously, it's a complex process and not all steps are described here. But in the end, we were able to come over the challenge and was able to migrate the project and get it working on [ASP.NET Boilerplate](https://aspnetboilerplate.com/) 5.0 and .net core 3.0

### Migrating from AWS DynamoDb to PostgreSql.

We have been using [AWS DynamoDb](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) to store Virtual File System with S3 Storage as backend. A combination of .NET SDK for DynamoDb and S3 was making it a really fun and easy development experience while building the same.

As we moved our system to production, bulk operations like renaming a folder, calculating folder size and moving files etc. were causing read and write throttling. We have been using a provisioned plan with auto-scaling up to 4000 operations but still wasn't performing bulk operations properly.

we tried to switch to on-demand capacity for the specific table but due to cost factors and low confidence of the bad experience, we decided to move on from DynamoDb table to PostgreSQL database as our team is more experienced in a relational database and it's always easy to get predictable results.

We used Hangfire Job to migrate data from DynamoDb table into PostgreSQL Table (Thanks to Bharat Sharma), and implemented the data access code to read/write using Entity Framework Core Code First approach.

### File sharing is not a simple problem to solve.

I realized in the last quarter of 2020, that file-sharing is still not a solved problem. Organizations still need a good file sharing strategy. In the age where there are tools specifically built for the same purpose like OneDrive, DropBox and many others, it's still difficult to hit the sweet spot of efficient, cloud-based, secure, and cost effective file sharing.

I've added it to my list of possible open-source project to come up with. Hopefully, my resolution to contribute to open-source through my open-source project will come to reality, and this can possibly be one of the projects that I would come up with in 2021.

### I read [Platform: The Art and science of personal branding](https://www.goodreads.com/book/show/40983156-platform)

This weekend, I finished reading [Platform: The Art and science of personal branding](https://www.goodreads.com/book/show/40983156-platform) by Cynthia Johnson.

I picked this book due to my willingness to develop personal branding and I was expecting a little more actionable ideas about the same instead of a success story. But I was impressed with the [game theory concept and it's use from the book](https://en.wikipedia.org/wiki/Game_theory). An example of using Twitter to build community was also innovative as I never thought to use Twitter like that. There many other pieces of advice that are helpful but you know them already if you are 30+ of age.

My search for the actionable book on Personal Branding is still on, please recommend a book if you know a good one!

### Health is wealth.

This week, I faced some bad news about unhealthy friends and family. Thyroid, Hypertension, High blood pressure, and allergic cold are all that my inner circle people struggled with.

Later during the weekend, I met my buddies and we agreed to develop a good habit of exercising starting very soon. **It's your lifestyle during your 35-45 years age which will decide how long you will live and how good that would be.** So, we will start with walking and cycling 20-40 mins a day and put in more effort to get together for such activities during the weekend as COVID-19 risk is reduced and we can go out with precautions.

**See you next week!**