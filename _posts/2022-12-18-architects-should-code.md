---
layout: single
title: Architects Should Code
categories:
  - architecture
  - development
tags:
  - architecture
  - development
  - culture
  - software
  - communication
excerpt: "No matter how far Architecture is from the code of applications: architects should always keep themselves active coders to fully understand the challenges of technologies and developers"
lang: en
ref: architects-should-code
---

Following the typical journey made by several architects, I too have started mine through coding software, when I was 10 years old, exploiting a [Commodore64](https://en.wikipedia.org/wiki/Commodore_64) I received as gift from my parents, originally intended for playing videogames: natural curiosity and some basic rudiments of hacking brought me to write my first program in [BASIC](https://en.wikipedia.org/wiki/BASIC), that had the function of adding two numbers.

Over the years I have developed those skills further, even employing them in unthinkable applications (such as writing my own [VST](https://en.wikipedia.org/wiki/Virtual_Studio_Technology) plugins for producing music), eventually ending up studying software engineering and making a career in the industry, as developer and later as architect.

At the moment of jumping the line that separates software development and business architecture, becoming a _Solution Architect_ I experienced several issues, since I had no access to the source code anymore, and I still had to organize solutions from the perspective of deliverables to higher functions of the organizations (_Product Managers_, _PMOs_, _VPs_, _CTOs_), employing non-technological language to explain technology challenges, which in the first part of that transition was extremely frustrating.

## Jumping the Line

![Architect not Coding](/assets/img/2022-12-18-architects-should-code/dilbert-ted-architect.png)

Despite of this transition to a more _business-oriented function_, I was still in the position of having to discuss with several teams of developers, to understand the scope of their work, the external integrations, the intentions of the architecture they (_voluntarily or not_) had established, and potentially bridging their efforts with the management functions of the organization, who had to ultimately allocate resources for those architectural components.

In few months my mindset about software development changed radically, once exposed to the organizational challenges of complex and large organizations, their strive to acquire resources, the aim for being competitive in difficult and challenging markets, and then I focused my attention more on the business aspects of the architecture, that I considered the foundation stone on top of which other activities (such as software development) were justified: [the Zeal of the convert](https://rationalwiki.org/wiki/Zeal_of_the_convert), one might say.

As a curious person I then intensified my knowledge and skills in Architecture ("_that big thing, whatever it is_" q.), standards, frameworks, tools, methodologies, shifting my focus from the code that I used to write (or at least review) on a daily basis: in fact, for about two years I stopped writing any single line of code, and I stopped caring for the low-level details of the technology (eg. _memory allocations_, _language improvements_, _new tooling_), that now became some sort of irrelevant information, in the scope of higher-level architecture choices.

The principle that _the higher you go, the less details you want_ has a rationale in the amount of information overload one might experience, if one would receive all the detailed information of anything happening in a large context: dealing with 10 different teams at the same time, while reporting to several management functions (CTOs, CIOs, VPs) and middle-management (Product Managers, Program/Project Managers), having to digest several sources of information, crunch them and produce myself some more, I thought that having to deal with the challenges of the code would have killed me.

## Back to Code

![Developer](/assets/img/2022-12-18-architects-should-code/programer-coding-on-laptop.jpg)

Anyway, it happened that I found myself in the situation of dealing with an architecture that touched two major concerns of _Organization Structure_ and _Access Control_, to establish a _forest_ of secured identities, in a complex SaaS context: after the analysis of the requirements (behaviors, security, products, finance, etc.), I did my researches on standard models, processes and technologies, scanned the market for potential vendors, taking down a rational target architecture for the matter (not very _agile_ as you can already spot).

It came the moment to face the (three) development teams who were supposed to integrate the technology in the existing environment, and eventually implement additional components to support it, trying to gather their inputs and feedbacks on the feasibility of the architecture (or rather: _trying to explain them how beautiful that solution was..._): unfortunately, their response was negative (or rather, _mixed, with skeptical notes_), and their initial approach was to get themselves out of their own issues, such as being under pressure for delivering that architecture, by implementing their own solution, without dealing with any of the principles, standards, technologies and best practices I had proposed.

Needless to say I was disappointed and caustic, frustrated by the situation and foreseeing the typical scenario of _reinvention of the wheel_ that causes a lot of embarrassment to organizations, wasted time, wasted resources, and shifts focus from core values to accessories that are not providing any real returns (opening to further issues): in that situation I really didn't understand how the developers couldn't foresee the rationality of the architecture, and the benefit that would have brought to them.

Full of frustration, after more than a month of discussions, back and forth between management, vendors, developers, I then decided to download a free IDE, and I started coding (in C#), during my free time, a [Proof-of-Concept (POC)](https://www.techtarget.com/searchcio/definition/proof-of-concept-POC) to demonstrate graphically and with code the logic and behaviors that I had intended, although through the mocking of the final providers.

I must confess that the exercise was fun, but also quite hard at the beginning: few years without dealing with _debugging_, continuous delivery, library scanning, performance tuning, made me feel again like the teenager me, who approached _Visual C++_ for the first time.

While I was writing the software solution I intended, I then realized some flaws in the model that I had designed before (eg. the role of _client applications_, or _the relationship between organizations and users_ and others), and then I realized myself the flaws in my communication to the developers, and the messages I was giving them, based on some abstractions, assumptions and theories coming from practitioners and vendors who were dealing with a different reality than the one we were into.

## Turning Point

Given the experience and the findings, knowledge and value extracted by the return to coding, should now I recommend every architect to go back to development to better provide to an organization? Well... giving a typical architecture answer, I would say: _'it depends'_.

Reading the master-piece ["Domain-Driven Design" by Eric Evans](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215) on the matter of designing and development, it is recommended to keep a separation between the designer (eg. _architect_) and the development team, unifying those parties in a common scope through _models_, _ubiquitous language_ and other elements: I believe it still makes sense, even for lower-level architects who have to deal with more technical details, but I also believe that more _business-oriented_ types of architects should not lose the touch with the technology, its capabilities, its challenges, and complexities, to better evaluate the alternatives provided in some solutions scenarios.

In more agile and lean organizations, the differences between architecture and development functions are minimal, and in most of the cases architects are involved in coding on a daily basis, applying their experience, design skills, modeling (process, application, data), infrastructure knowledge, and more, without any separation between them, the developers and the management: that I believe provides effective results, but it requires a small organization, using a single technological stack where everyone can relate to the code produced, the components employed in the architecture and the final goal. This kind of _agility_ is naturally not possible in more complex scenarios, where for example every department employs different technologies, or where the development departments are the result of mergers between organization with heterogenous technological stacks.