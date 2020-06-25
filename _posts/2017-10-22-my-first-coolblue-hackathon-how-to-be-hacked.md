---
layout: post
title: My first Coolblue Hackathon. How to be hacked
date: 2017-10-22 12:01:53.000000000 +02:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Code Development
tags:
- Hackathon
meta:
  _wpcom_is_markdown: '1'
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/AJsGSdoA1xX
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _publicize_job_id: '10599193547'
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:15487188;s:56:"https://twitter.com/joaoasrosa/status/922040353733177344";}}
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=27794317&stype=M&topic=6327806050770653184&type=U&a=PRUo
  _publicize_done_15638097: '1'
  _wpas_done_15487191: '1'
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2017/10/22/my-first-coolblue-hackathon-how-to-be-hacked/"
comments: true
featured_imae: /images/left-panel/blog.webp
---
Last week we had our annual Hackathon, my first at Coolblue. Here we are taken to a remote location for 3 days to hack away. I joined a team who wants to build an application to measure the happiness in Coolblue. Wait, measure happiness? How?

It's a straightforward concept: after a meeting, the participants click on one of the three available buttons, and the results are collected. Since the data is anonymous, we believe people will vote in an appropriate manner, giving insights about the mood of the group. It's a powerful tool, fits in our culture and can allow us to be proactive instead of reactive.

Day 1 - Being hacked
--------------------

Our team had a mix of skills, experience and expertise, and I was looking forward to starting the hackathon. In our first meeting, our Agile Jedi suggested using the [Pomodoro technique](https://en.wikipedia.org/wiki/Pomodoro_Technique), to timebox our activities. We all know, a hackathon should be a free flow, but sometimes the work drifts with people notice it.

![IMG_20171010_135327.jpg](/images/assets/img_20171010_135327.jpg)

Although not all elements knew the Pomodoro technique, after a brief introduction, the team was on board. For me was the first time to apply the method at team scale. :)

We outline the architecture, as well the components and technologies to use, and more importantly our goal. At the end of the second day, we need a fully functional prototype, where it is possible to vote in the context of a meeting and display the results per meeting. The team agreed to split it in half, handling the frontend and backend in separate streams. That kicked off our first Pomodoro!

![IMG_20171010_115856.jpg](/images/assets/img_20171010_115856.jpg)

Between Pomodoros, the team sat down together and discuss what we did, if we will invest more time on the task at hand, or even if we need to adjust or change the tasks to achieve our goal. Also, embody the agile spirit, here and there we had a broader discussion of adjusting the way we were doing the project, pretty much as a retrospective.

On the first day, I was working on the backend, doing part of our services infrastructure to support the application. We did lots of pair programming, on different fashions, and we speed up the development of our project. It allows us to be in constant communication, a key ingredient to a successful team. To share the components between the team members, we deploy the services in Docker containers with the help of Cake scripts. Hurray, scripting for the way!

![IMG_20171010_232703.jpg](/images/assets/img_20171010_232703.jpg)

On the first day, I was happy with our progress, we had the services and main application up and running. We were able to commit the changes to our repositories, build the services and application and running it locally using Docker. Now is time for the barbecue and a few beers with my colleagues.

![IMG_20171010_183555.jpg](/images/assets/img_20171010_183555.jpg)

Day 2 - Sleep is for the weak
-----------------------------

Sleep is for the weak. This was the motto for this year. And the room on the morning of Day 2:

![IMG_20171011_095248.jpg](/images/assets/img_20171011_095248.jpg)

After our breakfast and a morning walk, we decide to polish the UI of application and finish implementing the reports. I volunteered to work on the frontend, namely the display of the meetings reports. It has a chill morning, and we completed our application. Happy days, we need to prepare the demo for the Friday Hackathon Fair.

We laid down our strategy, gather some real-life data, generate our datasets and test the application in several machines, close to a real-life situation. We were tired, but with a smile on our faces, the mission was accomplished!

![IMG_20171011_182037.jpg](/images/assets/img_20171011_182037.jpg)

On the afternoon was reserved a hackathon activity, which involved being outside. We had a little competition in a bouncy castle. Good laughs.

![IMG_20171011_171048-1.jpg](/images/assets/img_20171011_171048-1.jpg)

After this relaxing moment, we head for our dinner. On the second day, he had a food truck. Excellent curry with a fresh beer.

![IMG_20171011_190135.jpg](/images/assets/img_20171011_190135.jpg)

The second day was almost wrap up, we had Hackathon party. Good vibes, some drinking games, an opportunity to know other colleagues from other domains.

Demo fair
---------

On the third day, we returned to Rotterdam, and we were given the afternoon off. However for me was the time to go to Amsterdam for TechDays. I will write about the conference in the following post. To showcase our projects, Coolblue hosted a demo fair on the next day in the afternoon. We had the opportunity to demo our application to our colleagues, showing the benefits of measure happiness. We had some interesting feedback to factor into the project.

![Image uploaded from iOS](/images/assets/image-uploaded-from-ios.jpg)

Final Thoughts
--------------

Personally, it was a great experience. 7 months ago I arrived at Coolblue (and to The Netherlands), and it was an opportunity to know my colleagues outside of my bubble. I had interesting chats, and today I know a little bit better other business domains.

Regarding the project, I liked to be hacked and be part of the experiment of applying the Pomodoro technique at a team level. It was an interesting experience in how a team can be in sync in a hectic environment as an hackathon. We keep our eyes on the ball, adjusting the work and at the same time having fun. Thanks, team! :)

To close this post, here is the video from the hackathon:

{% include youtube-player.html id=2QBmy1AmGvA %}