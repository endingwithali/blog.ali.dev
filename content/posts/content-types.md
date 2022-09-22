---
title: "Don't Forget Your Content–Type"
date: 2020-09-29
draft: false
summary: "A very brief exploration of Content-Type"
tags: [engineering]
---

I recently used the [EmailRep.io](http://emailrep.io) API on for a rapid prototype I was building. In heart of quick prototyping, I bypassed setting a Content-Type on my Fetch call:

```javascript
 await fetch( 'https://emailrep.io/'+{email}, {
    method: 'GET',
    headers: {
      'Key': {API KEY},
    },
  })
  .then((res) => {
    if (res.status !== 200) {
      return null;
    }
    return res.json();
  }).then((data) => {
    if (!data) {
      return null;
    }
    return data;
  });
```

Seems all good - should work fine. 

This was the response:

```json
Response {
  size: 0,
  timeout: 0,
  [Symbol(Body internals)]: {
    body: PassThrough {
      _readableState: [ReadableState],
      readable: true,
      _events: [Object: null prototype],
      _eventsCount: 2,
      _maxListeners: undefined,
      _writableState: [WritableState],
      writable: false,
      allowHalfOpen: true,
      _transformState: [Object]
    },
    disturbed: false,
    error: null
  },
  [Symbol(Response internals)]: {
    url: 'https://emailrep.io/example@test.com',
    status: 200,
    statusText: 'OK',
    headers: Headers { [Symbol(map)]: [Object: null prototype] },
    counter: 0
  }
}
```

The call returned with a status code of 200 OK, but the body contained a PassThrough object - an unexpected object type. I was confused - this was not the expected body and content as outlined in the API documentation.  How do I work with a PassThrough object? I couldn't find anything particularly helpful about this kind of object or what my problem was. 

Take a quick look at my API call - do you notice something missing? In my HTTP request headers.

I didn't set a Content-Type.

# What is Content-Type?

In June 1999, The Internet Society released a document - [RFC2616](https://tools.ietf.org/html/rfc2616) - outlining the Hypertext Transfer Protocol - HTTP/1.1. This document gives context, definitions, and best practices for working with HTTP.  HTTP/1.1 is no longer the standard - we are now on [HTTP/2](https://http2.github.io/). Many of the definitions and concepts outlined in RFC2616 are still the same as the HTTP/2 document was simply an update of the existing documentation for HTTP/1.1.

Content-Type is explained in RFC2616:

> The Content-Type entity-header field indicates the media type of the
entity-body sent to the recipient or, in the case of the HEAD method, the media type that would have been sent had the request been a GET.

In addition, Content-Type's [best practices](https://www.w3.org/Protocols/rfc2616/rfc2616-sec7.html) are also expanded on: 

> Content-Encoding may be used to indicate any additional content codings applied to the data ... that are a property of the requested resource. There is no default encoding.
> 
> Any HTTP/1.1 message containing an entity-body SHOULD include a Content-Type header field defining the media type of that body. If and only if the media type is not given by a Content-Type field, the recipient MAY attempt to guess the media type via inspection of its content and/or the name extension(s) of the URI used to identify the resource. If the media type remains unknown, the recipient SHOULD treat it as type "application/octet-stream".

Breaking this down, we learn that:
1. there is no default data encoding for the body of an HTTP request
2. setting the Content-Type when making an HTTP request is a should not a must
3. if the body type is unknown, treat the body as "application/octet-stream"

# Why do if 'should'?

Why should you explicitly set the Content-Type if it's only recommended? The clear definition of what kind of content you expect from the call helps you avoid the problems I had, as explained in the introduction of this post. 

![Dog dressed as business person, sitting at desk](/2020-9/1-sniff.jpg)

But, by not setting your Content-Type, you also open yourself up to a cross-site scripting attack.

## Cross-Site Scripting

Your application is exposed to Cross-Site Scripting (XSS) attacks when Content-Type is not set for API calls. An XSS attack is a type of web attack where attackers figure out a way to inject a script into your trusted website. This code will be executed and credentials / other private information can be collected through this attack.

By not setting a Content-Type header, you leave the interpretation of the content to content type inference algorithms (mime sniffing). Attackers can take advantage of this when there's the ability to upload content by including a malicious script in the uploaded file - which will then be executed upon rendering by the mime sniffing algorithm. 

To read more about Content-Type XSS attacks, I'd recommend reading this [Fortify](https://vulncat.fortify.com/en/detail?id=desc.dynamic.xtended_preview.web_server_misconfiguration_insecure_content_type_setting) post that goes detail about this type of attack.

# Conclusion

After spending a chunk of time spent trying to debug the API call, thinking it was a problem with [EmailRep.io](http://emailrep.io), it turned out my error was due the lack of Content-Type on the request. Simply including the line `'Content-Type': 'application/json',` in the header solved the problem and the call returned the expected JSON object. 

API and HTTP calls should not be a guessing game - take the guess work out of your calls and utilize Content-Type to ensure your return body is the expected type and you do not expose your website to malicious attacks.

# Bonus Content

Content aware scale is fun.

{{<youtube 7merzCPl-Xg>}}
