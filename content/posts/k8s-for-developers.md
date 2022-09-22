---
title: Kubernetes for Developers Who Know How to Develop
date: 2022-01-13
draft: false
tags:
- engineering
- backend
- kubernetes
- repost
---

Kubernetes is hard - We’re here to present it to you in a new light, specifically for developers, and why k8s can save you time.

This post was originally posted on the [New Relic Blog](https://newrelic.com/blog/how-to-relic/k8s-explained) and then cross posted to [Dev.to](https://dev.to/endingwithali/explaining-kubernetes-for-developers-who-know-how-to-code-1473)
---

You know how to program - you're in your first or second year of your first software engineering job. You've mastered the basics and are excelling at your job, but something's been bothering you. You keep hearing about this thing called Kubernetes being thrown around by another team. Kuber...netes? What does it mean?

After the third or fourth time you hear it, you decide to look it up. You get what it does, but you don't really get what it does.

Don't worry—I’m here to help.

Before we get started, I highly recommend [reading this article by fellow Relic John Withers](https://newrelic.com/blog/how-to-relic/what-is-kubernetes) - it's an excellent primer of basic colloquialisms and technical terms used when diving into the world of Kubernetes.

## Hi, welcome to the container store.
Most starter tutorials will explain how to deploy a basic "Hello World" server in the language of your choice. But it doesn't really do much except return an endpoint that says "Hello World.” What do you learn from that? Why is it always a web server?

Let's take a step back and remember that any type of application can be containerized and deployed using Kubernetes. Even the hit game from 2002, [Petz: Dogz 5](https://en.wikipedia.org/wiki/PF_Magic), can be run using k8s.

Does it actually make sense to put Petz: Dogz 5 into a container and deploy with Kubernetes? Maybe, maybe not. But say we wanted to run 10,000 instances of Petz: Dogz 5 or we wanted to access the game 10,000 times at once, all simultaneously. Then yes, using Kubernetes makes sense.

But Petz: Dogz 5 doesn’t use the internet. Kubernetes must require the internet, right? Not exactly. Connectivity is a must, but things like intranet allow for connection without using actual internet, creating isolated instances. Keeping it straight forward, while you can run things on k8s that do not need internet access, you’ll need connectivity in order to access the k8s cluster.

## Memenetes

Kubernetes has been the subject of memes...a lot. Why? Because in reality, setting up Kubernetes is hard. It's confusing and it takes a long time to get right.

![Evil Kubernetes be like shuts down containers when needed
](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/c8tnf6b2i8vmc7xf3cia.jpg)

However, once set up and configured properly, it's a powerful tool that can save developer time and application uptimes. 

So when should one start using Kubernetes? And why?

## Who? What? Where? When? Why? of Kubernetes

### Who? + What?
Technically, anyone can run anything using Kubernetes. Usually, you'll find it being utilized by DevOps teams to help scale their company's services to meet incoming demand.

### Where?
Kubernetes is run on a server (managing it yourself is known as “rolling your own Kubernetes”) or handled by vendor or cloud service provider as a managed Kubernetes.

### When?
Technically, you can start using Kubernetes on day one of building a project, but it doesn't matter when you start using it. The choice is up to the developers and the DevOps team.

### Why?
The ‘why’ question is where it gets a little more interesting.

Without Kubernetes, launching an application of any kind requires three different parts: 

- A compiled version of the code: provided by you and built in a form that can be easily run (such as binary). 
- An operating system: this might be your computer or something you set up manually, but could also be a container or use a buildpack. 
- A start command: The command used to execute your codes such as a binary or run statement. 

#### Kubernetes x Docker: Best Friends Forever

Whenever you hear Kubernetes, you're probably going to hear Docker in the same sentence. Kubernetes and Docker are like peanut butter and jelly—they're a perfect pair. Docker combines the three parts required to launch an application into one command. This makes it easier to deploy (or start) new applications through the creation of containers.

Containers are a critical part of the Kubernetes metaverse because they're the smallest building block of Kubernetes orchestration. Just like how atoms are the smallest bits of matter in the universe, pods are encapsulations of containers. Pods are considered a unit of one or more containers. All the containers in a pod will be co-located on the same operating system. 

#### Scale
Kubernetes can help make scaling your application easier. It's a distributed system that can automatically spin up new pods to help balance the load of incoming requests.

For example, you've just shared your side project on ProductHunt and HackerNews. As the creator, you're responsible for maintaining your side project's uptime and making sure that it works. It's starting to pick up popularity, and you see that your previous configuration is starting to max out at its ability to stay running. Did I mention that your project just blew up on Tiktok, and you've gone from 100 visits per day to over 10,000? It also just hit top of HackerNews - everyone is talking about it.

With the influx of users trying out your side project, you need to scale - fast.

Prior to implementing Kubernetes, you would need to go to your hosting site (either via a website for the cloud or on premises for non-cloud servers), manually provision the servers, run the containers, and set up the reverse proxies to handle incoming router traffic. With Kubernetes, this process is mostly automated. Since you were conveniently creating this side project to try to learn Kubernetes, you were prepared. To scale with the huge influx of demand, you're able to quickly update your Kubernetes config file to begin rolling out scaling changes for your side project.


## We've done it
As a developer, it's easy to forget to slow down, to get frustrated when learning new topics, and to gloss over asking why when one is confused. Hopefully, by reading this article, you've gained a bit more practical knowledge about Kubernetes and why you keep hearing about it everywhere you go.  

![Dog wearing glasses reading a book](https://newrelic.com/sites/default/files/styles/800w/public/2021-10/glasses-dog.webp?itok=K2jwKlKl)
  
## Next Steps
### Learn more:

Here are some excellent resources I'd recommend checking out if you're keen on learning more about Kubernetes from a highly technical angle:

- [Kubernetes from Scratch in Go by Liz Rice](https://www.youtube.com/watch?v=Utf-A4rODH8)
- [Kubernetes For Developers (A multipart series) by the team at Nirmata](https://nirmata.com/2018/02/07/kubernetes-for-developers-pods-part-1/)
- [Docker for Beginners by Travis Media](https://www.youtube.com/watch?v=i7ABlHngi1Q)
- [Why Kubernetes vs Serverless isn't a Real Debate by David Simmons](https://thenewstack.io/why-serverless-vs-kubernetes-isnt-a-real-debate/)
- [Kubernetes AutoScaler (AKA How It works) from Kubernetes.io](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)