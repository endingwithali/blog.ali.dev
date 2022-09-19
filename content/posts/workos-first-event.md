---
title: "T-30 Days To Our First Event"
date: 2020-08-25
draft: false
summary: "What we used to pull off WorkOS’s first event in less 30 days"
tags: [events, quarantine, professional, devrel]
---

Events in the time of Covid-19 are different. No more are the large rooms, free food, and the anxiety of “Am I going to the right place” after wandering through a corporate office for several minutes because you misheard the directions, took a left at the 3rd intersection instead of a right and are now completely lost.


![Bird looking at a map confused](/2020-8/1-workos-event-lost.gif)
*Me, trying to navigate through big tech offices*



When it came to the first event for WorkOS, a lot was on the line - we knew this event was the stepping stone for opening the door to more regular events, so it needed to go exceptionally well. There were grand ideas of what we wanted to do, but in the end of the day, one principal held true that allowed us to pull off our first event without a single problem to handle or fire to fight: **KISS (keep it simple, silly).**

# The Ideation

By talking with other event coordinators and members of the developer relations community, I learned that their events had low turn out rates: 30-50% attendance of people who registered. They found that due to COVID, employees weren’t being given the time to attend full day events across multiple days, and how easy it was to simply forget / skip an event. Instead of having to travel to a location, now you can attend an event from your living room, and it takes just a couple of click throughs to register. It’s a simple event in your calendar - it’s easy to skip.
We had a couple of iterations of what the event would look like before we settled on the final arrangement. 


At first, the event was to look something like an all day event: an hourlong keynote, parallel informational sessions (ran at least twice), live coding, live integration workshops, and then a large PR event. We were looking into using software like [Hopin](hopin.to) to host, along with cross streaming on to Twitch while utilizing OBS. However, as the date of the event came closer, the idea morphed and changed into something simpler.



![clown face and live coding](/2020-8/2-live-coding.jpg)
*I'm not saying don't live code, it just wasn't for us - for now*

For hosting the event, we looked into a lot of tech options - creating picture in picture presentations using mmhmm, creating looms to prerecord demos, OBS for video formatting, and even online conference software like Hopin to host the entire event. What we found most effective was using none of that - **KISS**.

# What Worked


First came the announcement and marketing. Figuring out our channels across which we can do publicity for the event was key: it wasn’t just the job of the marketing team. Every team member was asked to publish about the event across communities and channels they are actively involved in, for authentic growth and interest. In addition, we utilized Twitter and LinkedIn marketing, by sponsoring our event announcement posts.


To handle signups, we used [zmURL](zmurl.com). The easy-to-use setup, clean design, and well though out product features made it perfect, and being able to customize the event URL was a lovely touch. Using zmURL also means, yes, we did use Zoom to hold the actual event - specifically, we used Zoom Webinars.


Slides were designed in Google Slides, with support from our design team who created custom graphics for the event. Instead of live coding, we utilized simple code samples and demos. To generate code snippets, we use used [this slides code highlighter](https://romannurik.github.io/SlidesCodeHighlighter/) with the following theme:

```
{
	"bgColor":"#20242B",
	"textColor":"#D8DEE9",
	"punctuationColor":"#758A95",
	"stringAndValueColor":"#EBCB8B",
	"keywordTagColor":"#DB68E3",
	"commentColor":"#2FD085",
	"typeColor":"#9C27B0",
	"numberColor":"#46C2EC",
	"declarationColor":"#CA82BD",
	"dimmedColor":"#BDBDBD",
	"highlightColor":"#B92D2D",
	"lineHeight":1.5
}

```

The main slides were controlled by the host (for us, [Michael](twitter.com/grinich) and panelists shared their screen for demos - this helped simplify the transitions.


We settled on a simple day of schedule and format:
- 10:00 — Attendees arrive (intro music)
- 10:05 — Michael, CEO & Host, keynote
- 10:30 — SSO demo
- 10:45 — Admin Portal demo
- 11:00 — Directory / SCIM demo
- 11:15 — Magic Link demo
- 11:30 — Fireside chat w/ BrianneKimmel
- 12:00 — Close


![Picture of zoom meeting where Presenter is talking](/2020-8/3-livedemo.png)


Using a separate WorkOS specific account to host and manage the event in the background was very useful. The account carried out the formatting of the show - the video of the account was never turned on and the microphone was always muted. Between speakers, it would make sure to use the spotlight feature to highlight the live video feed of the person actively speaking. When speakers were done, the account demoted the user to attendee as to not clutter the panelist video panel.


![Picture of zoom](/2020-8/4-group.png)


Panelists / presenters were made co-hosts of the event - this is key for presentation based events. Being a co-host gives the user the ability to take over screen sharing, so each presenter had the ability to control their own demo. Once one presenter was done, a clear vocal queue like “Back to you Michael” gave clear indication for when the next person was to take over the screen sharing and turn back on their video feed.


In the Zoom Webinar, we kept chat and Q & A open to all, as well as allowed anyone to respond to the Q & A questions. This enabled any WorkOS teammate to be able to step up and answer audience questions. As questions were rolling in, the team was operating in the event slack channel establishing answers for questions and discussing the event in real time.


When it came to the fireside chat, all presenters were moved to attendees, and the speakers were promoted to panelist - this was done using the main host account. For the fireside chat, no presenter was set to spotlight.


![FIRESIDE CHAT](/2020-8/5-fireside.png)


Post-event actions broke down into video, outreach, and survey. The video of the event was downloaded, cleaned up, and distributed to the company YouTube channel for easy access. After the event, utilizing the Zoom Webinar features, we included an exit survey to receive feedback from attendees. Finally, we shared the video links, the link to the survey, and the opportunity to get started with WorkOS immediately to all attendee and people registered via email.


# The Final Result

We kept it simple - no fancy streaming sites, no fancy external software, minimal speaker switching. For a first event for a remote first company, the event went perfectly. There was not a single fire to fight, and have received high praise from attendees about how smooth the event ran (and also about how good the content we discussed was, of course)!

The final event ran without a hitch. We had over 50% attendance rate, and the event ran for just over 2 hours, including breaks.


I'm really proud of how the event turned out - a remote first team executing a remote first event. I plan on hosting more events in the future about enterprise readiness, so be sure to follow me on Twitter to get alerted!


Check out the final result below!

{{<youtube QOlJIHA04gs>}}



{{<youtube GybKjPBtVZI>}}



# Bonus Content


It's a 10.

{{<youtube SLP9mbCuhJc>}}






