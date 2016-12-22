---
layout: post
title:  "Lessons Learned Building Web APIs"
date:   2016-01-20 09:17:47 -0500
categories: web api
---
I’ve been working with Web API’s since 2009\. In that time I’ve learned a lot of useful lessons about what it takes to build a really good API. Let’s define the qualities of a “really good API”:

*   Low barriers to access
*   Quick to implement
*   Easy to understand

So what are some of the things that you can do as a developer to create one?

_Lesson 1: Design_

Your API should be nothing more than a gateway to your business logic layer. It will also provide a set of services on behalf of that layer. These include:

*   Catalog of consumer services
*   Data collection & transmission
*   Security & Authentication*
*   Logging & monitoring*

* start looking to use Micro services for these tasks

_Lesson 2: Routing_

A simple routing mechanism will make your API easier to use. It should be easy to configure. It should also allow multiple routes for accessing the same method. And of course, REST is BEST!

_Lesson 3: Avoid Hackable URL’s_

A hackable URL is one that has a pattern containing a data key that could lead to someone creating other URL’s with valid data keys.

For example, with http://mywebsite.com/orders/1234 it’s pretty easy to guess that 1234 could be an actual order or customer id. There are two practices that you can use to prevent this:

1.  Switch the route. Instart of using a route of /orders/{id} to /{id}/orders
2.  Change the ID to a unique identifier and perform a translation on that in the API

_Lesson 3: Responses_

You response is the primary interface of your API. It is the “I” in API. Your response needs to be

*   Easy to understand
*   Self-describing
*   Follows a consistent format​ (assume no one reads your documentation)

And when things go wrong (and they will) make sure that you provide your consumer both an error code and a friendly error message. It’s most likely that the developers that are implementing your API will never see a problem in testing. It’s usually their users that will find the problem. But who will that user blame, them or you? They don’t know about you. And you can quickly tarnish the reputation of your consumer. A lose-lose situation for everyone! So make sure that your error message can be understood by the actual user, the user of your consumer’s website.

_Lesson 4: Include Other Useful Information In Your Response_

Include a version number or build timestamp. Your API will evolve over time. And you will need for your consumer to have a way to quickly identify the version that thay are running.

Include the executing environment name (Development vs. Production). When your consumers start to build your API in thier system, you will most likely provide them a sandbox to work from. Once they are ready, they can switch to your production environment. But what if on Day 1 they forget to change the endpoint on their side? This has happened to me on more than one occaision. So provide them the environment name in your response and make them aware of this. This simple piece of information can help avoid a bad start.

Remember, anything that HELPS your consumer improves their experience. You goal is to make their experience as good as possible!

_Lesson 5: Limit Your Response Status Codes_

Trying to return too many HTTP status codes will only cause confusion. The fewer the status codes, the better. I can easily get away with just the following:

<table>

<tbody>

<tr>

<th>Status Code</th>

<th>Description</th>

</tr>

<tr>

<td>200 OK</td>

<td>Awesome!</td>

</tr>

<tr>

<td>400 Bad Request</td>

<td>The user of the API made a mistake</td>

</tr>

<tr>

<td>404 Not Found</td>

<td>What the user asked for was not found</td>

</tr>

<tr>

<td>500 Internal Server Error</td>

<td>The creator of the API made a mistake</td>

</tr>

</tbody>

</table>
<br />
_Lesson 6: Automated Testing_

Because Web API’s do not have a UI, they are well suited for both test driven development and automated testing. And as your API evolves, the test automation will allow for faster delivery of enhancements with fewer bugs.

I don’t get hung up on the type of test, be it a unit, functional or integrated test. I simply strive to have as much test coverage for as many scenarios as possible. I’ve found tools, such as
[Google Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en){:target="_blank"}, are very powerful both during development and acting as test runners replaying key tests.

And if there is anything that will save your company , it’s your test automation!

_Lesson 7: My Toolbox_

Outside of my IDE, I only need a handful of tools to assist me in my Web API development.

1.  Google Postman (see Lesson 6)
2.  Chrome Devtools
3.  [Fiddler](http://www.telerik.com/fiddler){:target="_blank"}
4.  [JSON Editor Online](http://jsoneditoronline.org/){:target="_blank"}
5.  [Wireshark](https://www.wireshark.org/){:target="_blank"}

_Lesson 8: Performance_

Dynamic Compression. That’s it. That’s been the most effective means of speeding up performance of my API. Every modern web server supports this and just about every browser. Simple and effective!

_Lesson 9: Versioning_

My approach to versioning isn’t about me, it’s about my consumer. They’ve made an investment in building my API into their website. It’s in my best interest to protect their investment.

_It’s not about me or my company, it’s about them!_

So the best strategy is an “add only” strategy. Add features that do not break existing ones. And should you need to add capabilities that would break your implementation, create a new version. I prefer to version my URL’s. If I need my current partners to move to that version, I plan a grace period for them to migrate to the new version. Never fear, they will wait until the very last minute to migrate. But be patient and realize that were it not for them, who would need your API to begin with!

_Lesson 10: Monitoring_

There will be problems, so planning on ways to diagnose those problems up front will pay dividends in the long run. Here are a few useful tips:

Log everything (preferably to a central data store for web farms)! Every incoming and outgoing response, every exception and anything else that you can think of. And don’t log to text files on individual servers. You’ll find yourself looking for a needle in a haystack!

Setup monitoring OUTSIDE of your network, even if it’s a simple API call that only returns a small response. It will help you know if your API is available.

And access your site continuously. This will help your API remain loaded in your web server’s memory, helping improve overall response time!

**API’s Need Consumers**

I know it sounds obvious, but when you put your consumers first, you will find that you remove the artificial barriers that can prevent them from using your API. You can have the most beautifully architected API in the world, but your consumers don’t care about that. They only care about getting results as fast as possible. You are competing for thier time and resources. So make them your priority, and I promise they will stay with you!

### Questions & Comments

Have a question about this post or anything else?
Ask away [on Twitter](https://twitter.com/stuartdga){:target="_blank"}.

