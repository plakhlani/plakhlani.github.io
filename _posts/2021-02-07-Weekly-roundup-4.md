---
title: "Experimentor Weekly Journal - 04"
date: 2021-02-07
image:
header:
teaser:
thumbnail:
og_image:
categories:
- Weekly
tags:
- Weekly
excerpt: "My weekly journal 04 - Converting ASPX to Web API, Outlook rules, Interviews, KGF and more"
---

My weekly journal is series of blog posts where I share stories about my professional and personal work. This is my weekly Journal 04, Feb 7, 2021, and in this post, I am going to share with you about:

1. Converting legacy ASMX/WCF services to Web API.
2. Outlook rules to forward emails to another account.
3. My struggle with taking interviews of Interns.
4. My unlimited love for the movie KGF: Chapter 1 


### Converting legacy ASMX/WCF services to Web API.
I have prior experience working with the challenge of converting a [Legacy ColdFusion web application to a modern single page application](https://www.faciletechnolab.com/projectdetail/Legacy-Coldfusion-Web-Application-to-Cloudbased-Modern-Single-Page-Application). But this time it was a new challenge where I get chance to work with converting legacy ASMX/WCF services to Web API. 

Well, for all of you who are new to ASMX services, it's an old school way of building web services through a service-oriented architecture. Service descriptions are published through specialized WSDL (XML) documents that help to discover and understand the services available for consumer clients. Simple object access protocol (SOAP) was used to perform the service operations and most of the time consumers were telling the services to perform some operations like get me a list of work centers, get me a list of work orders in progress, etc.

After the age of ASMX services, Microsoft introduced WCF services which gave options to build more secure web services that can be accessed via the internet or in the local network through TCP Binding.

Over the period, REST Services became popular and everyone started to adopt this new way of working with service-oriented architecture.

If you are further interested to know more about this, I will be publishing a detailed blog post about this in the future in our [Facile Technolab Blog](https://www.faciletechnolab.com/blog).

### Outlook rules to forward emails to another account.
Last week, I've posted about [AWS SNS and AWS CloudWatch for email notification on ECS](https://plakhlani.github.io/weekly/Weekly-roundup-3/#aws-sns-and-aws-cloudwatch-for-email-notification-on-ecs-going-down) and that worked so well.

The next challenge was tricky. We configured AWS Cognito with AWS SNS to send automatic invitation emails. As part of the customer onboarding process, it is critical to know if customers received an email invite and it's unprofessional to ask such things via email or call.

But, how do we know if an outgoing email is sent or bounced? Well, there are a couple of things that we tried. The first attempt was to create an SNS notification for every email that is sent or bounced. It took us a while to figure this out and thankfully, Barat Sharma from our team was able to configure it successfully.

But, the downside of it was, the SNS notification was not including which email is sent/bounced. So, just in case if you are on-boarding multiple customers, it was still a challenge to figure out which email is bounced and which one is sent. The simple solution for this was to on-board only one customer at a time and wait for SNS notification before a new customer is on-boarded.

This isn't a good solution from the end user's perspective. 

We started to look for a better solution and I noticed something interesting when I logged in to the outgoing email that we used for sending out an email. We are receiving a bounced notification email from AWS SES when the email is bounced. 

I configured the outlook rule to capture all emails that are coming from notification@aws.com and forwarded them to our team so that we know as soon as we have a bounced email while on-boarding a customer!

We were finally able to figure these things out after working iteratively. It was fun to try out all the simple and complicated solutions to finally get everything figured out.

### My struggle with taking interviews of Interns.
At [Facile Technolab](https://www.faciletechnolab.com/), we are growing fast as clients are liking us so much! That allowed us to extend our team and we decided to hire some interns. 

We were supposed to interview 25 candidates for the intern position and we were so excited about meeting and talking to the fresh talent in the industry. 

It didn't end up into that many interviews due to no shows (which is normal these days) but I was able to meet one intern who was impressive due to his determination to become a developer.

We will keep interviewing more interns and will be visiting another college campus next month to see if we can hire good talent that can be part of our team! 

### My unlimited love for the movie KGF: Chapter 1 
Last night, I watched [KGF: Chapter 1](https://www.imdb.com/title/tt7838252/), again one more time. I didn't finish it all but I watch at least 30 mins whenever this movie is played on the television. I like this movie so much because of its dialog, story, and excellently placed a sequence of events. I like this movie ever since it's released and was not so popular. But during lockdown last year, it becomes one of the most popular movies in entire India. 

I'm looking forward to [KGF: Chapter 2](https://www.imdb.com/title/tt10698680/?ref_=nv_sr_srsg_0) and watched the teaser release so many times already on youtube. 

**See you next week!**