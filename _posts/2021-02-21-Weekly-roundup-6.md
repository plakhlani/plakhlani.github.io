---
title: "Experimentor Weekly Journal - 06"
date: 2021-02-14
image:
header:
teaser:
thumbnail:
og_image:
categories:
- Weekly
tags:
- Weekly
excerpt: "My weekly journal 06 - "
---

My weekly journal is series of blog posts where I share stories about my professional and personal work. This is my weekly Journal 065, Feb 21, 2021, and in this post, I am going to share with you about:

1. ASMX to REST (Web API) and WCF to REST (Web API) migrations
2. Loss aversion
3. 

### ASMX to REST (Web API) and WCF to REST (Web API) migrations
[ASMX Services](https://docs.microsoft.com/en-us/troubleshoot/dotnet/csharp/write-web-service) used to be the only way to build web services in [Microsoft .net development](https://www.faciletechnolab.com/software-development-technology/microsoft-dotnet-or-donetcore-development). Developer used to write code in c# to support various business operations in the service. <code>GetWorkCenterList</code> or <code>GetWorkOrderList</code> etc. are simplest examples of such operations supported by asmx service. The asmx services were published in IIS, and was discovered through WSDL. In order to consume the service, you either generate a proxy through WSDL.exe if you are consuming it in [Microsoft .net development](https://www.faciletechnolab.com/software-development-technology/microsoft-dotnet-or-donetcore-development) or use language specific proxy generation tools in other programming. 

I have been doing [Microsoft SharePoint Development](https://www.faciletechnolab.com/software-development-technology/microsoft-sharepoint-onprem-or-online-development) and used asmx services supported by Microsoft SharePoint 2010 in order to read some lists or libraries in the [Microsoft SharePoint Development](https://www.faciletechnolab.com/software-development-technology/microsoft-sharepoint-onprem-or-online-development).

In a nutshell, [ASMX Services](https://docs.microsoft.com/en-us/troubleshoot/dotnet/csharp/write-web-service) supported implementation of service oriented architecture in [Microsoft .net development](https://www.faciletechnolab.com/software-development-technology/microsoft-dotnet-or-donetcore-development).

Due to tightly coupled SOAP dependency, XML serialization, data transformation and protocol specific complexities to implement security etc., Microsoft introduced [WCF](https://docs.microsoft.com/en-us/dotnet/framework/wcf/whats-new) which was new way to implement service oriented architecture in [Microsoft .net development](https://www.faciletechnolab.com/software-development-technology/microsoft-dotnet-or-donetcore-development).

[WCF](https://docs.microsoft.com/en-us/dotnet/framework/wcf/whats-new) provided many advantages over [ASMX Services](https://docs.microsoft.com/en-us/troubleshoot/dotnet/csharp/write-web-service) like interoperability, security and reliability, supported plain XML, REST and SOAP and much more. Now you can write programs in [Microsoft .net development](https://www.faciletechnolab.com/software-development-technology/microsoft-dotnet-or-donetcore-development) that supported both tcp based communication, http protocol based communication, REST communication, and SOAP all of it but you can still write code only once. Based on your needs you can enable any type of communication/transport securely.

With rise of .NET Core, Microsoft's [Unclear Plans for Server-Side WCF Continues to Frustrate .NET Developers](https://www.infoq.com/news/2019/06/WCF-Unclear-Future/). 

While there is no clear guidelines or help available on this topic, being a [Microsoft technology export company](https://www.faciletechnolab.com/), we already started helping our clients in migrating from ASMX and WCF to asp.net web api.  

### Loss aversion
I came across [loss aversion](https://en.wikipedia.org/wiki/Loss_aversion) while reading [Thinking fast, and slow](https://www.goodreads.com/book/show/11468377-thinking-fast-and-slow). In this week, I have been speaking to a friend about this and way to think clearly because due to [loss aversion](https://en.wikipedia.org/wiki/Loss_aversion), we feel almost double pain than the amount of happiness we receive when gaining something.

Later during the week, I also find another useful article on [loss aversion](https://thedecisionlab.com/biases/loss-aversion/) which may help better understand it.

Applying [game theory](https://en.wikipedia.org/wiki/Game_theory) is another helpful technique in many life situations if you can define your wins and loses clearly.

### 


### 

### 

### 


**See you next week!**