---
title: "How do web servers work?"
date: 2021-06-02
draft: false
summary: "I'm answering the question."
tags: [engineering,backend,servers]
---
_This article was originally posted on [Dev.To](https://dev.to/endingwithali/how-do-web-servers-work-54ci)._



Web Servers 

They're mystical things... You just, initialize one for your project, and it handles the rest. But what is actually going on under the hood? 

I got curious, so I asked my friend [Jonathan Kingsley](https://twitter.com/jfkingsley) if he knew about 'em. Turns out he's the kind of guy who read the [HTTP paper](https://tools.ietf.org/html/rfc2616) for fun, so we took to my stream and worked through building our own web server in Go.

Did I mention that the server is Mickey Mouse themed?

![Mickey Mouse whispering "thats a surprise tool that will help us later!" ](https://i.kym-cdn.com/photos/images/original/001/264/842/220.png "It actually doesn't use the theme at all whoops")

# HTTP

HTTP stands for "Hypertext Transfer Protocol"  - it was created as a part of the World Wide Web project in the early 90s.

> Tim Berners-Lee, a British scientist, invented the World Wide Web (WWW) in 1989, while working at CERN. The web was originally conceived and developed to meet the demand for automated information-sharing between scientists in universities and institutes around the world. - [CERN](https://home.cern/science/computing/birth-web)

This project has become the basis of how the internet works - it outlines the expectations of how to communicate data and information between servers. Your computer knows how to interpret websites because of the work of the World Wide Web project

![Ali with Tim Berners-Lee](/2021-6/alimeetshistory.jpeg)
A Picture of Ali meeting Tim Berners-Lee - [Original Post here](https://www.instagram.com/p/BSexBYvD5nv/)

# What did we make?

We decided to make two iterations of a "from scratch" web server - the first one, outlined in this blog post, handles get requests to endpoints that are hard coded. In another blog post, I'll walk through how we built a web server that can handle more dynamically implemented endpoints. 

# How does the server work?

## Main

### Listening

<img width="100%" style="width:100%" src="https://media.giphy.com/media/4HkkcZv2r5yCkkBDid/giphy.gif">

At the basic level, a web server [listens](https://golang.org/pkg/net/#Listen):

```go
port, err := net.Listen("tcp", ":1928")
```

We create a [Listener](https://golang.org/pkg/net/#Listener) object, `port`, that listens to a specific traffic port/communication endpoint for incoming requests of a specific [network protocol](https://www.w3schools.in/types-of-network-protocols-and-their-uses/). This line of code basically starts the server - you can now receive incoming requests. In this example, we are expecting TCP style requests on port 1928. (Mickey Mouse was created in 1928, therefore we chose to listen to port 1928!)

Great! We're done! Right?

Not exactly....

<img width="100%" style="width:100%" src="https://media.giphy.com/media/8TT8VjZTZGWQw/giphy.gif">


We can now receive requests, but how do we handle and read them, and how do we send back responses? 

### Accepting

```go
conn, err := port.Accept()
```

One of the [generic functions](https://en.wikipedia.org/wiki/Generic_function) that `port` has implemented is the `Accept()` function. [Accept](https://golang.org/pkg/net/#TCPListener.Accept) stalls/blocks until a new incoming request is seen by `port` - the incoming connection is returned as a [Conn](https://golang.org/pkg/net/#Conn) object. While the server is running, this function should be continually occurring - meaning that in code it is placed in an infinite `for loop`.

Yeah, you read that right - a time where an infinite loop is encouraged! 

### Handling

```go
go handleConnection(conn)
```

We create a new custom function, called `handleConnection` - this function is where we actually start going through, interpreting, and reading the data from the incoming connection. Each time there is an incoming connection from another client (aka any external connection since we are the server), we accept it and spin off a new handleConnection to deal with that client.

 

We use the keyword `go` to spin off [goroutines](https://golangbot.com/goroutines/), which enables [multithreading asynchronisity](https://stackoverflow.com/questions/34680985/what-is-the-difference-between-asynchronous-programming-and-multithreading/34681101) for the server. If we didn't use [goroutines](http://qvault.io/rust/concurrency-in-rust-can-it-stack-up-against-gos-goroutines) to enable concurrency, incoming requests that block will block everything on that thread, so you won't be able to serve as many incoming requests.  

### Code for main function

```go
func main() {
	fmt.Println("Goofy: hyuck - booting up!")

	port, err := net.Listen("tcp", ":1928")

	if err != nil { //failed to set up server
		fmt.Println("Mickey: Oh no Goofy! It looks like there was an error starting up the server! ")
		fmt.Println(err.Error())
		return
	}

	for {
		conn, err := port.Accept() 

		if err != nil { //client failed to connect with server
			fmt.Println(err.Error())
			return
		}

		go handleConnection(conn)
		fmt.Println("Welcome to the Mickey Mouse Web House!")
	}
}
```

<img width="100%" style="width:100%" src="https://media.giphy.com/media/Qgeg0wsKtgMjm/giphy.gif">

**Printing Twice**

```go
fmt.Println("Welcome to the Mickey Mouse Web House!")
```

When you run the code above, this print may occur twice. When browsers execute a request from a server, they execute separate requests for both the `favicon` of the page, and the contents of the page.

## handleConnection()

### Anatomy of an HTTP Request Message

According to the specifications of HTTP, there's required information that must be passed in a specific order in order to be properly digested by the receiving side. 

```css
GET / HTTP/1.1\r\n
Content-Type: text/plain; charset=UTF-8\r\n
Content-Length: <length>\r\n
\r\n
Hello World!\n
```

> Note: each one of these lines end with `\r\n` - when you're reading the incoming request, this allows the buffer to know where each line of the protocol ends. Basically, it helps separate new lines. 

```css
GET / HTTP/1.1\r\n
```

You can take this at face value. It tells the server the type of request incoming, the request target (the endpoint trying to be reached), and the HTTP version. 

If you want to read more about the anatomy of HTTP Messages, check out [this blog post](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages) by the team at Mozilla.

> 👋 I want to point out Content-Type header - up until I started working on this project, it didn't hit home as to why setting and checking `Content-Type` in HTTP requests was important. But now, I understand that each HTTP header acts almost like a basic if-else check point. Without setting the `Content-Type` specifically, the interpreting server won't know what to do or how to process the contents of the request. Processing each kind of request is basically hard coded. 
>
> <img width="100%" style="width:100%" src="https://media.giphy.com/media/X6QiVJjZWROHlTdiWX/giphy.gif">
>
> Basically, always check your `Content-Type` header if you're sending a request, and if you're processing/receiving a request, be sure to specify the expected `Content-Type` in your documentation to reduce frustration on both ends! 

### Anatomy of an HTTP Response Message

This is what an HTTP response message is expected to look like:

```css
HTTP/1.1 200 OK\r\n
Content-Type: text/plain; charset=UTF-8\r\n
Content-Length: <length>\r\n
\r\n
Hello World!\n
```

Let's break it down. 

<img width="100%" style="width:100%" src="https://media.giphy.com/media/cFSbwZr4i0hVe/giphy.gif">



```css
HTTP/1.1 200 OK\r\n
```

This line tells us what version of HTTP we are using, the status code, and the text associated with the status code

```css
Content-Type: text/plain; charset=UTF-8\r\n
```

This header tells the receiving client the type of incoming content so it knows how to handle it. 

```css
Content-Length: <length> \r\n
\r\n
```

The value for content length is important, because it helps the receiving side know when the receiving message has been delivered in its entirety. It ends with  double `\r\n` - the second one is a blank line used by request processors to note the start of the message body. 

```css
Hello World!\n
```

This is the message body! 

### Reading incoming requests

<img width="100%" style="width:100%" src="https://media.giphy.com/media/2sM0zOTQ2tjKo/giphy.gif">

```go
request, err := bufio.NewReader(connection).ReadString('\n')
```

We read the information from the incoming requests using a [bufio](https://golang.org/pkg/bufio/) object based on the incoming connection.  To keep the server as simple as possible, we're not even going to check what kind of [request](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) is coming in, only what endpoint is being requested. This allows us to only have to read the first line of the incoming HTTP request - we don't care what the rest of the request says. 

```go
requestParts := strings.Split(request, " ")
```

We split the incoming request into parts and check...

```go
if requestParts[1] == "/clubhouse" {
```

which endpoint is being requested. For this server, we're only accepting one endpoint: `clubhouse`. 

```go
message := "if goofy has a dog, and goofy is a dog....????"

connection.Write([]byte("HTTP/1.1 200 OK\r\n"))
connection.Write([]byte("Content-Type: text/plain; charset=UTF-8\r\n"))
connection.Write([]byte("Content-Length: " + strconv.Itoa(len(message)) + "\r\n\r\n"))
connection.Write([]byte(message + "\n"))
return
```

To send a response, we use the `Write` function of the [connection object](https://golang.org/pkg/net/#Conn) - but before we do that, we need to send our required headers (as outlined above and in the hypertext transfer protocol). 

If the incoming request is not looking for `/clubhouse`, then we send back a 404 error.

```go
connection.Write([]byte("HTTP/1.1 404 Not Found\r\n"))
connection.Write([]byte("Content-Type: text/plain; charset=UTF-8\r\n"))
connection.Write([]byte("Content-Length: 0\r\n\r\n"))
```

The final thing that happens before we finish the method is that we must close the connection

```go
defer connection.Close() 
```

In reality, this was the first thing we did in our `handleConnection` function - If you're new to Go, `defer` is a keyword utilized to describe a function that should be executed when the main function completes, no matter where it ends.

## Code for handleConnection()

```go
func handleConnection(connection net.Conn) {
	defer connection.Close()
	request, err := bufio.NewReader(connection).ReadString('\n')

	if err != nil {
		fmt.Println(err.Error())
		return
	}

	requestParts := strings.Split(request, " ")

	if requestParts[1] == "/clubhouse" {
		message := "If Goofy has a dog, and Goofy is a dog....????"

		connection.Write([]byte("HTTP/1.1 200 OK\r\n"))
		connection.Write([]byte("Content-Type: text/plain; charset=UTF-8\r\n"))
		connection.Write([]byte("Content-Length: " + strconv.Itoa(len(message)) + "\r\n\r\n"))
		connection.Write([]byte(message + "\n"))
		return
	}

	connection.Write([]byte("HTTP/1.1 404 Not Found\r\n"))
	connection.Write([]byte("Content-Type: text/plain; charset=UTF-8\r\n"))
	connection.Write([]byte("Content-Length: 0\r\n\r\n"))
}

```

{{<youtube lHhheCf0G1I>}}

[Final code on Github.](https://github.com/endingwithali/mickeymousewebhouse/blob/main/hardcoded/main.go)

# Serving Endpoints

I was surprised to learn that servers essentially just reading and parsing string. After years of working with them, I genuinely thought servers were way more complicated and that a simple example like this would be much more complex. 

Right now, our server can only handle one endpoint `/clubhouse` - which has a hardcoded response. What about dynamically implemented endpoints? Ones that are not defined directly in the server code - don't worry we've got that too. Blog post coming soon.

BTW, if you're curious if New Relic works with servers... yes it does. [Click here to learn more](https://newrelic.com/products/infrastructure). 

Special thanks to [Jonathan Kingsley](https://twitter.com/jfkingsley) for working on this project with me! Having a mentor to help walk me through this process and has made it very digestible! I am very grateful! 

Wish you could have seen this learning live? I stream coding and other fun tech things on Twitch almost every day. [Come hang out!](twitch.tv/endingwithali) See y'all soon!
<img width="100%" style="width:100%" src="https://media.giphy.com/media/JDTsqJhvLOq9G/giphy.gif">

### Mickey Mouse

Yeah... while this doesn't use Mickey Mouse for any kind of analogy, I've been working on my Mickey Mouse impression and the entire time Jonathan and I streamed this project, I kept doing my impression, hence the use of Mickey Mouse.

