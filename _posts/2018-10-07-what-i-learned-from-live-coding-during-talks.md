---
layout: post
title: What I learned from live coding during talks
date: 2018-10-07 20:01:50.000000000 +02:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Conferences
- Speaking
tags:
- Live coding
- Public speaking
- Soft skills
meta:
  _wpcom_is_markdown: '1'
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/YRv9XQU9WKo
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:15487188;s:57:"https://twitter.com/joaoasrosa/status/1048996884965199872";}}
  timeline_notification: '1538935314'
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _publicize_job_id: '22939087869'
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
  publicize_linkedin_url: www.linkedin.com/updates?topic=6454762581943943168
  _publicize_done_15638097: '1'
  _wpas_done_15487191: '1'
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2018/10/07/what-i-learned-from-live-coding-during-talks/"
comments: true
---
Last week, Kenny Baas and I, delivered 2 talks with live coding. We were at [NextBuild](http://nextbuild.nl/) (with [From EventStorming to CoDDDing](http://nextbuild.nl/sessions/from-eventstorming-to-coddding/)) and [Techorama NL](https://techorama.nl/) (with [Improving design and code quality with Property-based testing](https://sched.co/EjEe)).

![Badges](/images/assets/img_20181007_193500_01-e1538933946611.jpg) 

{:.image-caption}
*Conference badges*

In both talks, we used live coding as a tool to pass our message across the audience. It is useful, given the target audience is the developer community. The talks were IDE based, with refactors and new code. We didn’t have the need to deploy or run the code anywhere, apart for the tests, which ran from the IDE.

Here is what I have learned from the talks:

*   **If possible pair for the talk**. In both cases, we took a navigator/driver strategy, where one of us coded, and the other navigated the code. We both switched the roles from the talks, and when you are the driver it helps to be focused on the code, rather than code and navigate
*   **Practice a lot**. 2 weeks before, 1 day before, 2 hours before. And even then, you will get questions that you didn’t think of. If you can’t answer it, collect the questions, and go back to code, validating it after the talk
*   **Use local dependencies**. Our talks were in Java and .NET. Both ecosystems have package managers, which allows the usage of local dependencies. Prepare the dependencies on your local machine, for the event of Internet failure
*   **Have the coding script with you**. Take notes of the major points which you will code, in a small paper or post-its. It helps to have the “happy path” with you, for the event of a blackout
*   **Use the IDE light colour theme**. Every developer has her/his preferences regarding the colour scheme, but remember that you are delivering a talk. Is for your audience, not for you. The light colour themes work better for projections
*   **Use the default font**. Again, we tweak your development environments for our preferences; however, the default font shipped with our IDE is widely used, and (usually) is built on years of research
*   **Increase the font size**. Given that you will present the live coding session with a beamer, increase the font size for better readability. Ask out loud if the font size is good for everyone and tell the audience that they can interrupt if the font size is not good enough
*   **Allow questions from the audience on the spot**. We were lucky to have really sharp people on the audience. Before you start coding, tell the audience that they can ask questions as we go along. It makes our life “harder”, given that we do not know what people will ask, and we can deviate from the script. However, it creates a mob programming environment, where we can learn from each other. Again, people came for our talk, we are there to answer their questions
*   **Have a pen and paper available**. Sometimes you do not have the answer to the audience. It’s ok, no one knows everything. It is handy to have a pen and paper with you, allowing to take notes and move on
*   **Do a retrospective after the talk**. Right after the talk do a retrospective with the co-speaker (if you are doing it alone, it can be tricky). It is the best time to get insights on your blind spots, creating notes for further improvement on the topic

And that’s it. What are your learnings from talks with live coding? As a speaker or as an attendee, I would like to know your insights!
