---
title: Jamstack Is Dangerous for Beginners
date: 2022-09-12
categories:
- engineering
tags:
- jamstack
- cybersecurity
---

We need to be smarter about the way we talk about Jamstack in the context of junior engineers

---

*This is the blog post version of my Jamstack Security 101 Talk - [Click Here](https://www.twitch.tv/videos/1225257842?filter=all&sort=time) For the recording version *

Jamstack almost seems to be too good to be true - just Javascript, APIs, and Markup? Seems pretty simple to me! No more having to deal with on demand rendering of pages, server management, and BACKENDS? WHAT?

Just because new technology makes your life easier doesn't mean you can ease up on being vigilent with your security practices. You may seem like a small fish in a big pond, but you can never be too lenient on keeping yourself protected from potential attack vectors. 

## Too Good To Be True

One of the key tenets of Jamstack is moving as much rendering to the client side. In explanations of Jamstack you'll see sentences like the following thrown around:

> With no databases, plugins, or dynamic software running on your server, the potential for code injection and hacks is reduced enormously. [Source](https://builtvisible.com/go-static-try-jamstack/)
> 

Yet, just like the evolution of Javascript, we're finding more and more complex creations being built following Jamstack principals. (Did you know that in the beginning, javascript was written over a period of two days. Now it's critical to a huge majority of the internet) What does keeping your Jamstack application secure look like?

With so much happening on the client side, we need to remember what client side means - the person making the request to the website can see all the code that is executed on the browser, and can also manipulate that code. Client side is synonymous with client visible. 

## Serverless Functions

To separate your key protected API calls from your client side Jamstack application, use serverless functions. Or any kind of external server that cannot be discerned from the client side. 

Even then, how do we protect our serverless functions from external calls. No matter how many layers of serverless functions we put in front of our main function, code is code - there is a way to bypass. Below we discuss some ways to protect your serverless functions, both from the server side and the Jamstack side. 

### Protect your API calls

API calls are critical to Jamstack - It's literally what the A in JAM stands for. It's destructive to operate under the assumption that everyone knows to put your API keys in other places than the Jamstack application - especially when Jamstack touts the lack of a need of a backend. 

<aside>
💡 **Do not put your API keys in your Jamstack (client side) rendered API calls.**

</aside>

It seem's pretty obvious, but hindsight is 20/20 and we forgive those who forget :) What can happen if a malicious actor were to get their hands on your keys that you left in your client side rendered APIs:

- if they're credentials to a database or entity that store user information, clients will be able to get access to all that information
- if utilizing that API has costs associated with it, clients can use scripts to make repeated calls to build a large bill (a financial attack)

Both scenarios are not very fun to deal with. 

### Headers

[I've written about headers in the past](https://blog.ali.dev/engineering/2020/09/29/content-type/).  It's quite easy, when learning about web applications and coding, to sweep headers under the rug and forget to check and use them. Headers are actually quite powerful, and can help create more layers of protection for your API calls. 

Remember that time you were making an API for your webapp, and it kept throwing a CORS error - WHAT DOES THAT EVEN MEAN??? I'm here to help. There's a lot to unpack about CORS, but the gist of it is that CORS makes it such that only one origin can access resources. To learn more about CORS and the same origin policy, check out these two articles, [one](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) and [two](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS), from Mozilla.

Other headers that might be of interest include [HTTP Strict Transport Security Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security) and [X-XSS—Protection](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-XSS-Protection). 

### Authentication

If needed, you can protect your API calls by adding authentication to your Jamstack application. Authentication can be used on your [serverless function to validate requests](https://stackoverflow.com/questions/12296017/how-to-validate-an-oauth-2-0-access-token-for-a-resource-server) from your Jamstack application. There are two great articles on [CSS-tricks](https://css-tricks.com/apis-and-authentication-on-the-jamstack/) and [freecodecamp](https://www.freecodecamp.org/news/building-jamstack-apps/) that walk through adding authentication to your Jamstack application. 

### Rate Limiting

Another way to protect your serverless functions is rate limiting. Rate limiting is the action of liomiting a certain number of API calls to be made over a specific period of time. Rate limiting is effective for financial attacks because you can literally prevent repetative calls from happening to cause over billing. Rate limiting can be implimented based on location / IP address as well. To learn more about rate limiting, check out the following articles from [AWS](https://aws.amazon.com/blogs/architecture/rate-limiting-strategies-for-serverless-applications/), [Lihbr](https://lihbr.com/blog/rate-limiting-without-overhead-netlify-or-vercel-functions), and [Tyk](https://tyk.io/blog/ip-rate-limiter-middleware/).

### Monitoring

Monitoring is used to provide real time insights into what is happening on your application right now. With tools like New Relic, you can use these insights to learn about how your application is actively being used.  

Monitoring can be used to see if your serverless functions are being called too many times. Using alerts, tools like New Relic to let you know when your custom endpoints are getting an unexpected number of requests, or unusual patterns are detected. When abuse of endpoints does happen, you'll be alerted, and be able to react to the potential issues, keeping your application safe. If you're keen on learning more about alerting and New Relic, [click here](http://trynewrelic.com)!

### Tools

Security doesn't exist in a vacuum - free tools exist to help make securing your Jamstack website easier. You can use tools like [SSLLabs' SSL](https://ssllabs.com/ssltest) test and [webpagetest](https://www.webpagetest.org/) to quickly find potential security issues with your Jamstack application. 

### Sanitize Your Input

While using Jamstack websites may prevent code injection on the front end, that doesn't mean that you do not run the risk of injection when utilizing user input in your API functions. Be sure to properly sanitize your user input! 

## Conclusion

While this article focuses mostly on Jamstack API potential vulneratibilities, that doesnt mean you as a Jamstack application owner, are not vulnerable to the normal gamut of client side attacks. For example, everywhere you're taking in client submitted inputs, you sanitize it. If you're keen to learn more about securing your Jamstack application API, definitely check out [this article](https://stepzen.com/blog/how-to-secure-api-routes-for-jamstack-sites) by Carlos Eberhardt and [this article](https://blog.sqreen.com/static-websites-security/) by Don Goodman-Wilson.

Don't worry, even if things go wrong - it's not too late. [We can still turn the internet off](https://www.theguardian.com/technology/2014/feb/28/seven-people-keys-worldwide-internet-security-web). 

# Resources

- [stepzen.com](https://stepzen.com/blog/how-to-secure-api-routes-for-jamstack-sites)
- [raymondcamden.com](https://www.raymondcamden.com/2019/07/25/multiple-ways-of-api-integration-in-your-jamstack)
- [@franbuehler](https://medium.com/@franbuehler/owasp-devslops-journey-to-tls-and-security-headers-aa892f1ac851)
- [Perimeterx](https://www.perimeterx.com/)
- [Netsparker](https://www.netsparker.com/blog/web-security/content-security-policy/)
- [DataDome](https://datadome.co/bot-management-protection/bot-detection-how-to-identify-bot-traffic-to-your-website/)
- [Netlify.com](https://www.netlify.com/blog/2016/04/11/installing-your-own-ssl-certificates-a-step-by-step-guide/)
- [AWS](https://aws.amazon.com/certificate-manager/)