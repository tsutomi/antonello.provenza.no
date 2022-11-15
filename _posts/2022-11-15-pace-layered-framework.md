---
layout: single
title: Use the Pace-Layered Architecture to Align Efforts and Expectations 
categories:
  - architecture
  - products
tags:
  - architecture
  - application
  - methodology
  - gartner
excerpt: "Modern organizations aim for agility to deliver products, while dealing with expectations of control and finance forecasting"
---

It is very common, since more than a decade, that in organizations of a certain size (sometimes even in small ones) multiple and conflicting interests live together, driven by departmental objectives: for instance, _Product Management_ departments aims for new and successful products, _Developers_ aim for freedom to experiment with new methodologies and technologies, _Finance_ and _Management_ departments aim for control over budgets and for revenues.

In such a context it's easy for these organizations to enter in staling conditions, dispersing resources, not delivering on expectations, and thus reducing the planning horizon and opportunities.

## Different Systems, Different Expectations

![Manager Frustrated](/assets/img/2022-11-15-pace-layered-framework/angry-manager-leaving.jpg)

One of the most recurring situations I have been involved was the misconception of the nature of the _software systems_ acquired or developed by the organizations I have worked at: the tendency to put them all at the same level of planning, budgeting, architecture, description and management causes confusion and false (or wrong) expectations.

Some of you, who are reading this blog, probably already agree that separating systems by their nature, agility, product-orientation is natural, but you have to agree that for many this concept is not given: it is in fact not possible to control the development processes of an external organization from which we acquire licenses of a ready-made system (name one: [Salesforce](https://force.com), [Workday](https://workday.com), [Oracle](https://oracle.com), [SAS](https://sas.com), etc.), while at the same time we cannot avoid having control, introspection, planning and budgeting over the applications we develop internally.

We generally go outside on the market looking for _enterprise-ready_ systems and services (such as _SaaS_ solutions) that would alleviate our organization from the pain of developing, maintaining, operating and scaling established and common capabilities (eg. _customer management_, _billing_, _business intelligence_, _revenue assurance_, etc.), letting us able to focus on the core business (the _Value Streams_) of our organization.

In such discovery and market scanning, it is also very typical to enter in deals with providers of systems and services who require a prior long process of analysis, to better know the operative context in which their solutions would be employed, before signing binding agreements for multiple years, which include a number of objectives to ensure SLAs and penalties: procurement processes like these can be extended for months, involving multiple stakeholders, comparisons and _beauty contests_ between alternative providers, rounds of validation and approvals. Once such a system is acquired, the organization is compelled to use it within its processes for multiple years, electing it as a core component of its architecture, so that the pre-contractual investment and the operational costs to run it are justified.

A long, _waterfall_, bureaucratic, ritual process of such is in opposition with typically more _agile_ product development processes, made of fast iterations and continuous deployments of new commercial functions, _allergic_ to excessive regulations and blocks.

The above examples are just a couple of a myriad of others that would be useless to mention here, but I am sure you can name such situations (eg. _integration applications_, _proof-of-concepts_, _core business functions_, etc.), where resources, time and methodologies of management are wrongfully allocated.

## Gartner's Pace-Layered Application Strategy

The fact you encountered such scenarios, probably more than once, and like you several other organizations, says of the recurrency the problem, that led one of the main providers of analysis services ([Gartner](https://www.gartner.com)) elaborated [an architecture framework](https://www.gartner.com/en/documents/1890915) to guide organizations towards a rational addressing the issue.

![Gartner Pace-Layered Strategy - Applications](/assets/img/2022-11-15-pace-layered-framework/systems-1930.jpg)

Observing patterns and best practices applied by various large organizations, it was possible to categorize and rationalize the different kind of systems employed or developed, coming to three main types:

* **System of Innovation** -  In this category enter those applications that are implementing short-living innovations, such as _Proof-of-Concepts_ (PoC), marketing campaigns websites, experiments.
* **System of Differentiation** - Categorizes those systems implementing industry-specific functions, or functions provided uniquely by the organization (here examples may vary a lot, from _core banking_ systems, to SMS messaging routers, to health analysis systems, etc.)
* **System of Record** - Includes those systems that manage core information records of the organization, such as billing systems, CRMs, ERPs, etc.

This classification is not just an empty _tagging_ for reports and statistical analysis, but in fact drives some of the most important dynamics of a company, when allocating resources, applying change control methodologies and planning: acquiring this clarity is crucial for achieving better harmony between departments and stakeholders (although the ambition of _peace_ is still an utopistic state, since the persisting interests of the individuals).

Identifying the kind of systems we deal with is also beneficial to appoint the correct responsibilities to the various stakeholders involved: if an externally acquired system cannot be internally controlled, but rather integrated, the demand to a technical/development departments and teams to own that system, handle the relationships with the provider, goes easily out of scope.

### A Flavor for Each One

In the matrix below, Gartner visually simplifies the various elements applicable in the strategy of management of the systems.

![Gartner Pace-Layered Strategy - Matrix](/assets/img/2022-11-15-pace-layered-framework/gartner-pace-layer-matrix.jpg)

Thanks to the above summary, it's easy to notice how formalities, requirements and engagements reduce when we move from the handling of _System of Record_ to the _System of Innovation_.

In fact, you can recognize how the results of innovative initiatives are hard to forecast, since they might represent some new ways of handling the business from the organization, or even from the whole industry, that is hard to predict: managing such efforts as an established _line of business_ would cause wrong allocation of resources and time, instating false expectations in the stakeholders.

Anyway, to compensate the freedom provided to innovation, this is restricted to a shorter temporal overview, limited generally to cycles of 1 or 3 months.

In this operational context applications are developed without any integration to the production environments, to limit the risks of affecting customers with the high instability given by immature systems, unsure planning, rapid changes.

Architects operating in such an environment should be _hands-on_ on the everyday's development process, being part of the team, rather than focusing on the formalization of the architecture of the applications, since the high pace of changes: I have personally used this construct to produce myself proof-of-concepts to showcase some methodology on security or the implementation of a product, terminating the project right away, once handed to the proper organization.

## Categorization of Systems

As you have understand by now, the classification of system of your organization in one of the three kinds (_System of Innovation_, _System of Record_ or _System of Differentiation_) has an important impact in the management of the resources within an organization, the mastership of information, the flow of the data and as such CIOs should spend a considerable amount of time and focus on their correct identification.

It would be then easy to imagine that this job is (or should be) an easy task, to be concluded in few hours, involving just a handful of people, but it's in fact not that easy.

Some of the questions to answer when performing this activity include:

* _Which system masters our core data?_
* _Can we outsource functions to off-the-shelf systems?_
* _How much funds are reserved for Innovation?_
* _What is the maturity of the organization?_

Depending on the people involved in the analysis, the political environment and the readiness of the organization as a whole, some evident classifications might be rejected.

### Transitioning Innovation to Differentiation

One of the most typical degeneration of an innovation process within an organization is the so-called _premature productification_, that is the situation in which a _Proof-of-Concept_ (or another type of immature application) is acquired by the business functions of the company (_Product Management_, _Sales_ or similar), with no regard for the challenges of an intentionally weak and unstable architecture, assuming it as capable of handling production charges.

It is important for architects to be aware of such situations, making aware the overall organization about the challenges of innovative processes and _Systems of Innovation_, to avoid situations of such, that is a _though sell_ in agile environments, where principles of _Continuous Delivery_ set the ambitions of the management of having always innovative solutions in the portfolio.

With this regard, I would like to separate what it is a _System of Innovation_, as described by the Gartner's framework, from the _innovation in established systems_: it should be possible for mature systems to allow for extensions (through _open-close patterns_), _feature toggling_, _A/B testing_ and other kind of exploration of the innovations, but these capabilities should be provided within a _well-architected_ context of functions not affecting the established functions of the system.