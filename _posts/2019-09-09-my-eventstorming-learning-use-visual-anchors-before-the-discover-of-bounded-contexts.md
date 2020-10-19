---
layout: post
title: 'My EventStorming learning: use visual anchors before the discovery of Bounded
  Contexts'
date: 2019-09-09 22:18:51.000000000 +02:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Visual Collaboration Tools
tags:
- Bounded Context
- EventStorming
comments: true
excerpt: EventStorming is a visual collaboration technique, invented by Alberto Brandolini. This post will not go into the details of EventStorming, and you can find useful resources on the web. Instead, I will share learning from the many sessions that I facilitated!
---
[EventStorming](https://www.eventstorming.com/) is a visual collaboration technique, invented by [Alberto Brandolini](https://twitter.com/ziobrando). This post will not go into the details of EventStorming, and you can find useful resources on the web. Instead, I will share learning from the many sessions that I facilitated!

One of the forms of EventStorming is Big Picture. It aims to convey the knowledge across different silos, capturing what's in people's minds. During a Big Picture session, it is normal to see Bounded Contexts emerging. Wait, what is a _Bounded Context_?

Bounded Context is a strategic design pattern described by [Eric Evans](https://twitter.com/ericevans0) in his seminal book "[Domain-Driven Design: Tackling Complexity in the Heart of Software](https://www.amazon.com/exec/obidos/ASIN/0321125215/domainlanguag-20)":

> "Multiple models are in play on any large project. They emerge for many reasons. Two subsystems commonly serve very different user communities, with different jobs, where different models may be useful. Teams working independently may solve the same problem in different ways through lack of communication. The tool set may also be different, meaning that program code cannot be shared.
> 
> Multiple models are inevitable, yet when code based on distinct models is combined, software becomes buggy, unreliable, and difficult to understand. Communication among team members becomes confused. It is often unclear in what context a model should not be applied.
> 
> Model expressions, like any other phrase, only have meaning in context.

{:.image-caption}
*Quote from [DDD Reference](http://domainlanguage.com/ddd/reference/), from Eric Evans*

However, by the nature of a Big Picture session, we start in a Chaotic Exploration mode, where the language is fuzzy, and boundaries (apparently) don't exist. Thus, as a facilitator, I want to capture as many knowledge as people have, before given structure.

After the Chaotic Exploration, the group enters into the phase known as Enforcing the Timeline. At this point, the group starts to discuss the events and builds a coherent story. Usually, at this point, the boundaries emerge, but not always.

For those cases, it's good to use some visual anchors, as scaffolding for further exploration. As example:

![Example of a visual anchor for a Big Picture EventStorming session - © All rights reserved](/images/assets/img_20190905_145030.jpg)

{:.image-caption}
*Example of a visual anchor for a Big Picture EventStorming session - © All rights reserved*

It is useful for use cases, where the group (or organisation) is in a scale-up mode. Although there are some specialists in some parts of the process, the process doesn't cross silos because they don't exist!

What I experienced is that this visual anchor helps the group to reason about parts of the process, enabling a discussion about the different boundaries within a process; it makes it easier to reason and discover those bounded contexts.

What are your experiences when facilitating modelling sessions such as EventStorming? Any tips or clue?
