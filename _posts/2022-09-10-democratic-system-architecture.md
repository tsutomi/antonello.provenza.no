---
layout: single
title: "Democratic System Architecture Design - The C4 Model"
category: architecture
tags:
  - architecture
  - system
  - c4
  - agile
excerpt: "Defying the challenge of letting developers to document the architecture of the systems through the development phases and versions"
---

Mature organizations require the documentation of the architecture of their systems, for several reasons, like _compliance to regulations_, _cross-team collaboration_, _system design_, although such documentation process is tedious and tends to produce material that goes outdated quickly: because of these and other factors, especially within environments that embrace an _Agile_ culture, the production of architectures, and the whole architecture process, is biased and opposed / discouraged.

## The Architecture Dilemma

![Perplexed Woman - Dilemma](/assets/img/2022-09-10-democratic-system-arch/perplexed-gloomy-smart-woman.jpg)

A _product-focused_ culture (such as implemented in _Agile_ environments) requires fast iterations, continuous delivery and fast response to user and market demands, that is the core value for an organization, but such approach also increases the possibility of introducing dangers of various kinds, like _data security breaches_, _privacy infringements_, _monolithic designs_ (hindering functional scalability and causing difficult management after a short period of time).

While business functions of enterprises demand a long-term visibility (_3-7 years_) of the systems life-cycle, enough to allocate and secure resources through strategies, commercial functions instead focus their attention and efforts on the short or mid-term (_3 months to 1 year_). Furthermore, operational functions within the organization have an even shorter sight (_hours to days and weeks_), dealing with _everyday's issues_.

Since the proximity of the system and solution development teams to the commercial and operational functions, even embedding them in some Agile environments, the tendency of software developers within such setups is to minimize, or even remove, architecture thinking, planning and revision from their processes, given the perception that these would slow the production and delivery.

This perception is not completely untrue, although exaggerated: the _architecture process_ can be long and complex, involving several stakeholders and external providers, especially when dealing with large organizations, and at higher level of details; anyway, it can also be lean and faster paced than expected, depending on the _layer_ in which this is applied.

The process of design of a system's architecture, or its revision, is in fact an important step within the development of core functions or the integration of externally provided functions of the organization: provides information to members of the development teams, to other architects, to product owners, quality and delivery managers or other operators (security, support, etc.).

Neglecting the production of such deliverables, or letting them go out of date, opens up to some risks for the organization, hindering collaboration between parties (thus replication of functions), hiding security and privacy breaches, or even causing regulatory infringements.

## C4 at the Rescue

![C4 Containers](/assets/img/2022-09-10-democratic-system-arch/bigbankplc-Containers.png)

Documenting a system architecture easily maintainable, clear to read, communicative and effective, has been the challenge for many years, moving from [UML](https://uml.org) to [ArchiMate](https://pubs.opengroup.org/architecture/archimate3-doc/), which partially achieved their goal, helping architects and _initiated_ people to communicate to each other's with ease, using the common standard provided to describe processes, applications, relationships.

Anyway, such effort was always addressed to receivers with an academic knowledge of the principles of software architecture, its processes and deliverables, excluding those stakeholders without a specific practice with the matter: this contributed to architecture being seen as _important, but unknown_.

In the attempt to resolve such issues of complexity, the Software Architect [Simon Brown](https://simonbrown.je/) iteratively (from 2006 to 2011) elaborated a new model, putting together the principles of the  _UML_ and the _4+1 Architectural Views_, publishing it with the name [C4](https://c4model.com), under a _Creative Commons_ license.

This model acquired immediately a lot of popularity among those development leaders, architects and developers who belonged to _Agile_ organizations, since its simplicity (5 only elements), and ease of use through tooling.

![C4 Models](/assets/img/2022-09-10-democratic-system-arch/c4-elements.png)

To summarize here the model is composed of simple elements:

* **Boundary** - Represents an arbitrary boundary of an enterprise, a project or a system
* **Container** - A container of functions and controllers, that can be represented generically or as a _Database_, _Web Application_ or _Web Browser_ (when containing scripts that are relevant)
* **Person** - The entity interacting with the system's components (either a physical person or an application)
* **External System** - Describes a system that is externally defined and which internals are not known (and/or not relevant) for the designer
* **Relationship** - Unlike other architecture models (defining multiple types), a generic relationship between elements (_Containers_, _Controllers_, _Persons_, _External Systems_): this can be of any kind, unilateral or bilateral

While more comprehensive and descriptive models like [ArchiMate](https://pubs.opengroup.org/architecture/archimate3-doc/) provide precision to the definition of Enterprise Architectures, C4 focuses rather on the definition of systems, their immediate integration context, their internal components (often ignored by EAs)

## Integration Benefits

Although it was born as a model that could've been easily drawn on a whiteboard during a meeting,as mentioned above, the real success of C4 as a collaborative model was achieved thanks to the tooling provided by the author himself ([Structurizr](https://structurizr.com)), or by extensions to existing tooling, such as the [C4 extension](https://github.com/plantuml-stdlib/C4-PlantUML) to [PlantUML](https://plantuml.com/) engine: thanks to them, the architecture representation shifted from a drawing practice, demanding important amount of time, attention and dedication, to a _textual-based coding experience_.

In particular, the possibility of embedding the C4 architectures into [Confluence](https://www.atlassian.com/software/confluence) (_de-facto_ the most used knowledge-base wiki among industries of every kind), speeded up the adoption of the model for the visualization and display to the organizations.

A collateral benefit of such approach is the possibility to leverage the versioning of architectures through regular [Git](https://git-scm.com/) repositories, and eventually the integration (after textual parsing) with wider Enterprise Architecture repositories (such as [Ardoq](https://ardoq.com) or [iServer](https://www.orbussoftware.com/iServer)).

In fact I have personally produced and consumed [decorated C4 architectures](https://github.com/plantuml-stdlib/C4-PlantUML) using [Visual Studio Code](https://code.visualstudio.com), integrated by the [PlantUML Plugin](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml): this allows the automatic rendering of the graphs, while focusing on the textual notation of the architecture.

## Conclusions

Organizations shouldn't be shy to adopt an architecture process at the system design and development level, fearing the problematic of slow processes of production, iteration and maintenance: such processes are bringing clarity and reduce risks of over-engineering, bad decisions, and misalignments in the design and development.

Adopting an easy and effective model such C4 by the software development functions (_Tech Leads_, _Senior Developers_, _Product Owners_) aims to simplify and demystify the topic of architecture, often seen as a bottleneck in the delivery of value, while enhancing the collaboration and knowledge of the overall architecture of the enterprise, reducing risks on several aspects.