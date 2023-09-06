---
title: Resume Based Development
excerpt: "Projects and services are sometimes built by architects and developers to look good on a resume, not to solve a problem."
layout: single
date: "2023-09-03T07:25:34+01:00"
categories: [architecture, development]
tags: [architecture, development, organization, process, software, devsecops, risk, patterns]
ref: resume-based-development
lang: en
---

Projects and services are sometimes developed by architects and developers with the sole intention of enhancing their resumes, rather than addressing real problems. This practice poses significant issues as it results in wastage, frustration, technical debt, and the creation of unmaintainable code.

<!--more-->

## The Dynamics of Resume Based Development

![Resume](/assets/img/2023-09-03-resume-based-development/resume-apply-work-form.jpg){: .align-center }

Organizations with an established agile software development process are more susceptible to encountering a _resume-based development_ approach. This vulnerability arises due to the significant autonomy afforded to agile teams in determining both what to build and how to build it.

One of the fundamental skills to seek in a developer is the ability to learn new technologies and frameworks. Consequently, developers are frequently provided with opportunities to acquire these skills. Regrettably, this sometimes results in the adoption of trendy and _hyped_ technologies and frameworks that do not serve the immediate problem.

Occasionally, this choice is motivated by a genuine desire to equip the organization with a modern, future-proof solution. However, in many instances (as per my experience, the majority), it represents a _self-serving_ decision aimed at enhancing the developer's resume for internal career growth or external job prospects.

### Overengineering Solutions to Problems

Assuming a well defined structure of an agile team, where the product owner has a clear vision of the product and good grip on the marker, the implementation of the service(s) that provide the functions of the product is left to the team, in which one of the developers is generally the _architect_, meaning the one who ultimately makes the architectural, technical, decisions.

In this phase of inception, the acting architect might use the opportunity given by the _green field_ solution to experiment with new technologies and frameworks, which is not necessarily a bad thing, but it can lead to the adoption of a solution that is not the best fit for the problem at hand.

I had to face myself several occasions where the implementation of a service was overengineered to experiment with a new technology, implementing quite simple requirements with a very complicated and unknown approach, or even worse not achieving the goal at all.

## The Impact on the Organization

![Colleagues Having Headache](/assets/img/2023-09-03-resume-based-development/group-business-colleagues-having-headache.jpg) {: .align-center }

Working with mature technologies and frameworks surely provides benefits like _predictability_, _support_, _patterns_, while at the contrary adopting innovative approaches to the implementation of services introduces a lot of _uncertainty_ and _risk_.

Product managers, product owners, and business analysts, are often not aware of the technical implications of the choices made by the team, and they are not able to assess the risk of adopting a new technology or framework, which is often not even mentioned in the requirements: here the relationship and trust between parties is key to avoid the adoption of a solution that is not the best fit for the problem at hand.

The uncertainty and risk associated with the adoption of new technologies often lead to a slower development pace and, in the worst-case scenario, project failure - a significant waste of both time and resources for the organization.

### The CQRS and Event Sourcing Example

A few years ago, before [CQRS](https://martinfowler.com/bliki/CQRS.html) became a well-known pattern, I encountered a situation in which one of the developers responsible for the _architecture_ of a critical security component, vital for the large-scale solution I was working on, chose to implement it using _CQRS and Event Sourcing_ as a greenfield solution, contrary to my recommendations to rely on mature technologies such as [Active Directory](https://en.wikipedia.org/wiki/Active_Directory).

None at that time, either within the organization or in the industry, knew CQRS and Event Sourcing well, and I had to study the pattern myself, to understand the implications of the choice made by the developer: given the uncertainty and risk introduced by the adoption of a new pattern, and the lack of any vendor to support it (in fact, the developer himself implemented a framework to support it), I asked him and the organization to desist and adopt a more mature technology, but I was overruled.

Two years passed by, through implementations, experiments, failures, without the component to ever be functional, with an enormous waste of time and money for the organization, and with the developer to leave the organization, leaving the component in a state of _limbo_.

Ultimately, the organization decided to scrap that component from the architecture and to adopt a more mature technology, with a reputational damage for those who supported the expense to support and immature technology, to implement a component from ground up, not representing the core business of the organization, and even failing to deliver it.

## The Architecture Bias

Superficially, some organizations consider the role of an architect just the realization of designs and diagrams, to provide a set of _work packages_ to the developers, and to review the code produced, with a naive approach to what the deliverables of an architecture should be. Some organizations even consider the role of an architect as a _senior developer_, who is not involved in the complex assessments of _IT strategy_ and _IT governance_, worried that this might slow down the delivery of the product.

Being an architect is not just about dealing with code patterns, performance and scalability, but it is also, and more prominently, about considering the whole context in which a service or a component is introduced, the IT strategy of the organization, the costs failures and recovery: in many occasions, these responsibilities have been stripped out of the role of an architect, and the role has been reduced to a _senior developer_. Or even worse, some developers have been granted the title for internal career advancement, without the proper skills and experience.

I am not exonerated from this bias, since I must confess that I failed myself in the past to consider what the architect role meant with this regard, and I have been guilty of the _resume based development_ approach myself, at least in one occasion: we learn, we grow, we improve, we share our experience with the aim of helping others to avoid the same mistakes.

## Architects Make it Boring

One of the main criticism towards architects is that they make things boring, and this is true: architects are not there to make things exciting, but to make things work, and to make things work in the most efficient way, with the least amount of risk and uncertainty.

The choice of adopting new technologies and patterns to implement a service is not necessarily a bad thing, but it should be done with the right approach, with the right assessment of the risk and uncertainty, and with the right support from the organization: impact of a failed delivery ripples its effects through the whole organization, and it is not just a matter of the reputation of the architect, but of the whole cohort of people involved.

### The Innovation Stream

![Developer at Work](/assets/img/2023-09-03-resume-based-development/javascript-developer.jpg){: .align-center }

Developers are generally (and hopefully) attracted by innovation, experimentation, and learning: being in a job where you can be excited by the opportunity to learn new technologies, free from the burden of risk, is a key motivator for developers to join a company, grow with it and stay.

Regrettably, the adoption of new technologies and patterns does not always proceed smoothly, and success is not guaranteed. While offering a secure environment for innovation within the organization is vital for attracting and retaining talent, it is equally crucial to prevent the adoption of new technologies and patterns from being solely driven by the _resume-based development_ approach.

Mature organizations allocate resources and time to the _innovation stream_, where product development teams feel safe to experiment with new technologies, evaluating their complexity and risks, learning from the experience, and sharing the knowledge with the rest of the organization.

Implementing such a process is an important investment for an organization, which is not assured to provide a return, and it cannot be taken lightly: in fact, only few large organizations can afford to have such a process in place, and it is not a surprise that they are the ones that are able to attract and retain talents.

Unfortunately, the vast majority of organizations should instead accept to rely on mature technologies and patterns, and to provide their developers with the opportunity to learn new things in their spare time, or by attending conferences and meetups, or by providing them with a budget to attend courses and training: in such contexts product owners and architects act in their role of _governance_ trying to reduce risks from the adoption of innovative technologies that are not proven to be the best fit for the problem at hand.
