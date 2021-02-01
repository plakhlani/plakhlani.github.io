---
title: "Experimentor Weekly Journal - 03"
date: 2021-01-31
image:
header:
teaser:
thumbnail:
og_image:
categories:
- Weekly
tags:
- Weekly
excerpt: "My weekly journal 03 - SharePoint Forms Authentication, Finshots.in, AWS SNS and AWS Cloudwatch, reading a book, and more"
---

My weekly journal is series of blog posts where I share stories about my professional and personal work. This is my weekly Journal 03, Jan 31, 2021, and in this post, I am going to share with you about:

1. Forms Authentication in SharePoint using LDAP for external authentication.
2. AWS SNS and AWS Cloudwatch for email notification on ECS going down.
3. Articles I've gone through.
4. I started reading [Sapiens: A Brief History of Humankind](https://www.goodreads.com/book/show/23692271-sapiens)
5. Things I learned.

### Forms Authentication in SharePoint using LDAP for external authentication
If you have ever worked on things like [Extending SharePoint beyond your organization](https://www.faciletechnolab.com/Blog/2017/2/26/extending-sharepoint-beyond-your-organization), one way to achieve the same is to use Active Directory to store external users and use Forms Authentication to allow external users to login to your SharePoint through a custom login page.

In last week, I was helping one of the clients resolving their issues. They were using Forms Authentication with LDAP built by some vendor with who they were no longer in contact. Suddenly, one day they started seeing issues with the ability to add new external users to the site collection and adding permission to allow them access.

This was critical to them as this capability was used by their employees on day to day basis and they have a process to strictly store files in SharePoint. No file sharing via email.

I teamed up with the client, with one of our [SharePoint Expert Developer](https://www.faciletechnolab.com/software-development-technology/microsoft-sharepoint-onprem-or-online-development) and helped them resolve this issue. The problem was, they were manually adding Membership provider for LDAP into web.config, and every time SharePoint Time Jobs run some operation that requires re-provisioning of web.config operations, it was wiping out the manual changes causing the issue to re-appear.

The solution was to create a Web.config modification and deploy it through a feature so that SharePoint remembers it properly.

#### References:

- [EXTENDING SHAREPOINT BEYOND YOUR ORGANIZATION](https://www.faciletechnolab.com/Blog/2017/2/26/extending-sharepoint-beyond-your-organization)
- [How to Configure Forms-Based Authentication with AD in SharePoint 2010/2013](https://wiki.deepnetsecurity.com/pages/viewpage.action?pageId=1411571)


### AWS SNS and AWS Cloudwatch for email notification on ECS going down.

I'm part of the team where we use [AWS ECS](https://aws.amazon.com/ecs/) for an internal business portal used by some employees to automate their daily tasks. We have set up an Azure DevOps build Pipeline that creates a docker image and uploads it to [AWS ECR](https://aws.amazon.com/ecr/), updates the  [AWS ECS](https://aws.amazon.com/ecs/) tasks to set their number of desired instances to 0 and then 1 again.

This was all going so well. But, for any reason, if any of the ECS cluster containers goes down, the business portal behaves unexpectedly. We wanted a facility so that any time anything happens to the ECS cluster host or container, we receive a notification.

I have done a little research and found a good straight forward article to achieve the same in AWS Documentation that helped me achieve the same. [Here is the article](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs_cwet2.html).

Now, every time any of the containers or hosts goes down from any environment, our team receives a notification. 

As a bonus advantage, I found that there are a couple of containers which was going down every time they are hitting with the first request due to misconfigured memory limit. I was able to fix it quickly. I found a couple of more problems related to configuration due to these alerts and I'm glad I did this.

I'm now relaxed because, in the future, all the employees with seeing better performance, quality, stability and would have fewer problems in their day-to-day life as automation will work smoother! 

### Articles I've gone through.

- [Finshots Special - You only live once](https://finshots.in/archive/gamestop-reddit-retail-investors/?utm_source=finshotsDaily&utm_medium=ZerodhaMarkets): My brother-in-law [Shyam Kanojia](https://github.com/shyamkanojia) originally told me about this, and then Zerodha sent me a newsletter where I found "Reddit vs Hedge Funds" article from Finshots.in which caught my interest. 
- [https://bloggerspassion.com/guest-posting-sites-list/#technology-blogs](https://bloggerspassion.com/guest-posting-sites-list/#technology-blogs): I was looking for guest posting and found this good list of guest posting sites that I'll be using for my own purpose.
- I'm subscribed to [Finshots](https://finshots.in/) to keep in touch with all the financial world news in India.

### I started reading [Sapiens: A Brief History of Humankind](https://www.goodreads.com/book/show/23692271-sapiens)

I'm too early to say anything but I wanted to read this book due to my special interest in historical stories and how it's being told in various ways. Stay in touch and you will see my book review for this book in the upcoming weekly article.

### Things I learned

I want to share some things that I've learned hard ways:
- Laminating any important document isn't a good idea. Removing lamination from a document costs 500x more, time-consuming and risky process. I advise never laminate a document.
- Use + signs while subscribing to various sites with your email to separate out them in Gmail. For example, I used lakhlaniprashant+reading@gmail.com email while subscribing for Finshots last week and now I can easily make emails from Finshots skip inbox and fall into a separate reading list that I'll go through once a week during the weekend.


**See you next week!**