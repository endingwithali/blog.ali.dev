---
title: Testing with Images in Javascript
date: 2019-03-28
categories:
- engineering
tags:
- javascript
- images 
- testing
- medium repost
---

How to import an image in Javascript to be used in Jest Tests


_This article was originally posted on [Medium](https://medium.com/@endingwithali/testing-with-images-in-javascript-52fcbe06961f)._

---

<p style="margin-bottom:0;"><br/></p>
<pre style="margin:0; padding-top:2em;">
<center><iframe src="https://giphy.com/embed/BgrAbwtpqknXW" width="480" height="262" frameBorder="0" class="giphy-embed"></iframe></center><center>How I feel working with Javascript sometimes</center>
</pre>
<p style="margin-bottom:0;"><br/></p>


# The Story
I was assigned with writing tests using images for an endpoint I created at work. The tests and endpoints were written in Javascript using Jest and Node.js, respectively. I figured it wouldn’t be too difficult — opening a file or image is something I’m familiar with in Java and Python, but the only experience I had doing this in Javascript was when there was a frontend available to pass in the image information. I had some idea of how to do this, so I was determined to figure it out on my own instead of turning to others to get the direct answer. But, as we all know — knowing how to do something in one language doesn’t mean you understand how to do it in another language. I ended up struggling to figure out exactly how to open the image and be able to pass it as a variable and convert it to base64 without acquiring it from a frontend.(Spoiler alert: I ended up asking people)

# The Process
In order to clear up exactly how to do this, I turned to the place (almost) everyone turns to when they have a question: Google.

I executed a total of 31 unique queries. I also ended up asking two separate groups of people for how to do this:

include image in javascript test body
<br/>
image as variable javascript
<br/>
image as variable javascript testing
<br/>
image as variable javascript backend
<br/>
javascript test with image
<br/>
javascript test with image backend
<br/>
javascript access image
<br/>
javascript react imge
<br/>
handling image as variable javascript
<br/>
image representation in code
<br/>
image in code
<br/>
javascript json binary object
<br/>
transfer binary data json javascript
<br/>
javascript send image to server
<br/>
javasript image
<br/>
javascript image from file
<br/>
javascript image from local file
<br/>
access local image javascript
<br/>
use image for testing javascript
<br/>
read image javascript frm file
<br/>
mock image javascript
<br/>
**_ask friends_**
<br/>
filereader
<br/>
javascript filereader
<br/>
javascript filereader image
<br/>
javascript filereader example
<br/>
javascript filereader image testing site:stackoverflow.com
<br/>
javascript image blob
<br/>
javascript create blob from image local
<br/>
read image from fille javascript filereader
<br/>
read local file filereader
<br/>
jest test with image
<br/>
json send image
<br/>
**_ask coworker_**
<br/>
base 64 to buffer
<br/>
readFileSync

# The Final Solution

It was a total of two lines of code. Use the method [`readFileSync`](https://nodejs.org/api/fs.html#fs_fs_readfilesync_path_options) and then convert to a 
base64 string. In code:

```
var imgFile = readFileSync(pathToImage)
var fileStr = imgFile.toString(“base64”)
```

For those curious, `readFileSync` returns a type of `type { ext: 'jpg', mime: 'image/jpeg'}` which can then be converted to `base64`.

Simple.

I hope this article helps you streamline your image working process, and save you 31 unique Google queries.
