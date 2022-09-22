---
title: How to do Subdomain URL Redirects with Vercel Hosting
date: 2022-01-25
draft: false
summary: Create cool branding and quick redirects using Vercel!  
tags:
- engineering
- serverless
- hosting
---


---
I remember the first time my friend Ash showed me [Vercel](https://vercel.com/) (at the time it named Now / Zeit). I was blown away. Since then, I’ve been using it to host my personal blog and personal website - both [ali.dev](http://ali.dev) domains. 

One of the things I’ve been meaning to do over the past year is create subdomains for quick branded forwarding to different websites. There isn’t a straightforward tutorial on how to do this, so here we go!


<center><img width="50%" style="width:50%" src="https://media.giphy.com/media/IzjhI7ggjDlEnMxZMu/source.gif"></center>

<br/>

# What you’ll need

- Vercel Account
- Github Account
- Custom Domain

This tutorial assumes you’ve already purchased your custom domain, and are managing it via Vercel. If this is not the case, please check out this document on [custom domains on Vercel.](https://vercel.com/docs/concepts/projects/custom-domains) 

In this project, I will show you how I created a redirect for the subdomain, [live.ali.dev](live.ali.dev), to my Twitch channel - [twitch.tv/endingwithali](twitch.tv/endingwithali). I actually wrote this blogpost live on my stream, using an Oculus Rift! I've included a clip of it below.

{% youtube 'https://youtu.be/Bz0PJ-n4Gy4'%}
<br/>


To write this blog post, I refered to [this Github issue](https://github.com/vercel/vercel/discussions/5622) that was opened on Vercel's repo by [SeinopSys](https://github.com/SeinopSys). 

1. Create a basic GitHub repo for the domain 
    ![It's the basic page for creating a new repo on github](/2022-01-25/vercelrd-1.png)
    
    ![it's the basic github page after a new repo has been created](/2022-01-25/vercelrd-2.png)
    
2. Initialize the project locally - it won’t need much in it. 

3. Create a document in the local folder called `vercel.json` - this is the only file you will need for redirects. 
    
    ![terminal command line touch vercel.json](/2022-01-25/vercelrd-3.png)
    
4. In `vercel.json`, add the following code: 
    
    ```json
    {
        "redirects": [
            { "source": "/", "destination": "[https://twitch.tv/endingwithali](https://twitch.tv/endingwithali)" }
        ]
    }
    ```
    
    This JSON object says that every-time the ‘/’ domain is visited, Vercel will redirect the visitor to the destination URL. I wanted all visitors of the page to be immediately redirected to my twitch channel hence, `"destination":"https://twitch.tv/endingwithali"`.
    

5. Commit code to the Github
    ![terminal with code being commited to a github repo](/assets/images/posts/2022-01-25/vercelrd-4.png)
    
6. Run the `vercel` command in your terminal to create a new vercel project. Make sure it’s a new project, not linked to any pre-existing project

7. Run `vercel --prod` to push your website live.
    
    ![terminal showing project being deployed to vercel and to prod](/2022-01-25/vercelrd-5.png)
    

    At this point, your redirect will be live, but not have the proper domain. In the next steps, we will set up the domain. 

8. Go to your Vercel Dashboard ui (online, click into the project)
    ![dashboard of the live ali dev project](/2022-01-25/vercelrd-6a.png)

9. Connect your Github repo to your project by clicking:  
    ![dashboard of vercel project showing the git integrations](/2022-01-25/vercelrd-6.png)

    We are connecting the project to the Github repo, because Vercel has it such that every time a commit is made to your repo, it’ll update the website. This makes it easier to update the URL as needed. 

10. Next, click into `settings` > `domains`

    ![dashboard showing the vercel project domains that are available](/2022-01-25/vercelrd-7.png)

11. Add the domain you want to redirect - for the subdomain, you can just type in the subdomain. The main domain should be maintained / controlled by the Vercel name servers. [Click here to learn how to set that up.](https://vercel.com/guides/transferring-domains-to-vercel)
    ![dashboard showing the successful successful setting of the domain for the vercel project](/2022-01-25/vercelrd-8.png)
    
12. Congrats you now have a domain redirect!

Go forth and redirect all the pages! 

<center><img width="50%" style="width:50%" src="https://media.giphy.com/media/9T1LrOu1A2ipq/source.gif"></center>
<br/>


# Bonus Video

{{<youtube RH1ekuvSYzE>}}
