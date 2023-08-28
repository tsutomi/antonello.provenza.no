---
title: The Dynamics of Emerging Architecture in Organizations
layout: single
excerpt: "Organizations are complex and layered systems, where applications and services are the result of designs over time and not of a single architectural vision."
tags: architecture, organization
category: architecture
date: "2023-08-28T08:23:22+01:00"
lang: en
ref: dynamics-of-emerging-architecture
---

Simple organizations, especially those who are in a _startup_ phase, are usually characterized by a small number of people, who are able to cover multiple roles and functions, and where the communication is direct and informal.

The design of the overall architecture of the systems, applications and services consisting the organization is usually the result of a single vision, which is often the result of the founder's experience and knowledge, and the result of the first implementations of the organization: these are usually easy to change, adapt, and evolve, since they are owned by a single person or a single team.

In such a scenario, the _enterprise architecture_ is usually not a concern, since the organization is still small and the systems are not yet complex enough to require a dedicated function, the technological stack is usually homogeneous and the communication between the different components is direct and simple.

## Moving to the Next Level

When the organization starts to grow, the number of people involved in the development of the systems increases, and the number of systems and applications increases, the complexity of the overall architecture increases, and the need for a dedicated function to manage it becomes more and more evident.

To such a complexity and _growth pain_, it is usually added the need to maintain the existing systems, which are usually not designed to be easily changed, since they were typically implemented to serve an immediate need, and not to be part of a long-term strategy: such systems are usually called _legacy_ systems, and they are usually the most difficult to change, since they are the result of a _[legacy architecture](https://en.wikipedia.org/wiki/Legacy_system)_.

In several situations, I found myself approaching the source code of some of these applications, to trying make sense of the design choices, and I found myself wondering _'what were they thinking?'_. In fact, the design of such systems is usually the result of a _[design by committee](https://en.wikipedia.org/wiki/Design_by_committee)_ approach, where the different stakeholders of the organization, with different backgrounds, knowledge and objectives, have contributed to the design of the system, without a clear vision and strategy. In addition to this, it is typical that the most senior technical figures who led the design of such systems had no training in the best practices of software design, and they were usually the most senior developers, who were promoted to the role of _technical lead_ or _architect_.

Anyway, organizations who grow face new problems and challenges, often underestimated and not considered in the initial design of the systems, and they are forced to adapt and evolve the architecture of their systems, to make them more resilient, scalable, maintainable and secure.

For example, a growth in the number of users of a system might require to scale the system horizontally, to increase the number of instances of the application, to serve the increased number of requests, or to scale the system vertically, to increase the capacity of the existing instances, to serve the increased number of requests, or to acquire services from external providers, terminating some functions currently implemented in the system.

## The Emergence of Architectures

The evolution of the architecture of the systems of an organization is usually the result of a series of _emergent_ designs, which are the result of the _emergent_ behaviors of the organization, and not of a single architectural vision.

As much as one might want to academically state that the architecture of an enterprise can be clearly defined and designed, the reality is that the architecture of an organization is the result of the _emergent_ behaviors of the organization itself: choices are taken by decentralized teams, with the ambitions of solving the problems they are facing, and not of designing the overall architecture of the organization.

These dynamics within the organization are usually the result of the _[Conway's Law](https://en.wikipedia.org/wiki/Conway%27s_law)_, which states that _'organizations which design systems ... are constrained to produce designs which are copies of the communication structures of these organizations'_, and it's particularly observable in _Agile_ organizations, where the teams are self-organized and autonomous, and they are not constrained by a centralized architecture function, producing a multitude of services and applications which implement each one a specific set of patterns and practices, reflecting the skills and knowledge of the team who designed and implemented them, rather than a coherent and consistent architecture.

Enterprise Architects who belong to such organizations should resist the impulse to _rationalize_ and operate any _military force_ to restrain such movements, frustrating the values and mission of the organization, that intentionally has chosen such technical paths, but rather try to make sense of the _emergent_ architecture, trying to identify the patterns and the commonalities between the different systems, and trying to identify the best practices and the standards to be applied to the different systems.

I never found it productive trying to impose a _top-down_ approach to the design of the architecture of an organization, going against the existing asset of people, skills and systems, but rather trying to influence them, by providing the teams with the right tools, standards and best practices, to make them more effective and efficient, communicative and collaborative.

## Mixing Intentional and Emergent Architectures

As mentioned above, successful organizations grow and evolve, and with them the enterprise architecture of the systems they are composed of: this means that large portions of the functions implemented internally (eg. CRM, ERP, communications, etc.) are usually replaced by external services, externalizing costs, risks, resources, and focusing on the core business of the organization.

In such a scenario, the core function of Enterprise Architects is to design _intentional architectures_, setting the target for the integrations and the interactions between the different systems, assessing ahead of time the target state of the final architecture, and then working with the different teams to implement the required changes.

How can then a successful organization can mix the _intentional architecture_ with the _emergent architecture_?

The answer I have given myself (without any ambition of being the right one), is to make _intentional architecture_ as _emergent_, providing the teams with the right tools, standards and best practices, to make them more effective and efficient, communicative and collaborative, so that the skillset of the teams can be leveraged to design and implement the architecture of the various components forming the target architecture, achieving a good level of _buy-in_ from the various parts of the organization, especially those who are more resistant to change (such as the development teams, who are usually more focused on the short-term objectives, rather than the long-term ones).

## Collaborative Design

Although it is not always possible to control precisely the design of the architecture of an organization, it is anyway possible to influence it, by providing the teams with the right tools, standards and best practices, to make them more effective and efficient, communicative and collaborative: ultimately, the sharing of the common knowledge, patterns, practices and standards, will make the teams more effective and efficient, and will make the architecture of the organization more consistent and coherent.

For an organization, keeping the set of principles, standards, technologies (aka the _"IT Strategy"_) consistent is a matter of cost control, investment opportunities, resource management, and ultimately of _[technical debt](https://en.wikipedia.org/wiki/Technical_debt)_: the more the organization is able to keep the _IT Strategy_ consistent, the more it will be able to control the costs of the systems, the investments in new technologies, the management of the resources, and the reduction of the technical debt.

## Managing the Expectations

The core aspect to manage when applying such an _agile_ approach to enterprise architecture is the expectations of the stakeholders of the organization, who are usually expecting a clear and defined architecture, with a clear and defined roadmap, and not an _emergent_ architecture, which delegates responsibilities of the design to the teams, low in the organization chart and level of details.

Not only the management of the organization would likely oppose this view, when hiring an Enterprise Architect, but also the teams themselves would not like to be charged with such a responsibility, since they are usually focused on the short-term objectives, and not on the long-term ones.

In fact, the quick assumption that might come up is "if the teams are the ones designing the architecture, what is the role of the Enterprise Architect?".

The concept of "architecture" was imported into software development from the construction industry, where the architect is the one who designs the building, and then the construction workers are the ones who build it, following the design of the architect: this parallelism had (and in some, very niche, contexts still _has_) a meaning following the _waterfall_ approach to software development, where the design of the architecture is done upfront, and then the development teams are the ones who implement it, following the design of the architect.

In today's _Agile_ world of IT, the design of the architecture is not done upfront, but rather it is done _emergently_, and thus the role of the Enterprise Architect has changed as well, becoming a coordinator of the design process, rather than the designer: that is something to be communicated and understood by those organizations who strive in situations where _agility_ is perceived as a necessity to attract talents, but on the other hand they are suffer the consequences of such choice (eg. lack of control, lack of visibility, lack of predictability, etc.).
