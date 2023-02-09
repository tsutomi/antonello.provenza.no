---
layout: single
title: Self-Sustainable DevOps
categories:
  - architecture
  - devops
tags: [architecture, devops, devsecops, communication, openapi, interfaces, client, microservice]
excerpt: "Medium and large organization face the issue of collaboration between teams and services: clear boundarie and responsibilities are crucial for success"
---

## Teams and Services

One of the most foundational elements in _Enterprise Architecture_ is the definition of _Application Services_ (to be deistinguished from the _Business Services_), that represent the IT implementations supporting the _Value Streams_ of the enterprise: clear scopes, boundaries and functions are crucial for the best efficiency of the organization.

Considering the architecture of a stereotypical e-Commerce system produced by an organization, represented in the following graph

![eCommerce Service](/assets/img/drafts/eCommerce%20Architecture.png)

In the _Service Layer_ of the architecture we can observe the presence of four core services:

* Customer Service
* Catalog Service
* Order Service
* Checkout Service

They might have been implemented by one single person (_hopefully not!_), one single team or by several teams and they likely integrate each others through internal interfaces (behind the public _API Gateway_ stereotype), to move information between them, as needed.

The popular [Team Topologies](https://teamtopologies.com/) methodology assigns design, implementation and operations responsibilities over _systems_ and services to teams, according to their orientation (as _Stream-Aligned Teams_, _Platform Teams_, _Enabling Teams_ and _Complicated Sub-system Teams_), so that they can own a certain area of interest and collaborate with each other, producing coherent and consistent products for the enterprise.

This organizational methodology emerges from the well-known [Conway's Law](https://en.wikipedia.org/wiki/Conway%27s_law), that states

> Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization's communication structure

In fact the focus on the communication and collaboration of teams within an enterprise is crucial for producing valuable and consistent outcomes, and such problem has been considered with several approaches.

## Service Interfaces

One of the neglected aspects by teams owning an entire system (eg. _The e-Commerce System_) or a single service (eg. _The Catalog Service of the e-Commerce System_), is the consideration of this artifact (_system_ or _service_) will be consumed by others, by a programmatic perspective.

When working _Graphical User Interfaces_ (GUI) a lot of effort is employed to do research on the user behaviors, mocking target and producing graphical elements, since the identification of a clear _persona_ as a user of a system, that activates one or more services with its interactions through those interfaces (eg. _Selecting an item from the catalog_, _Checkout and paying for the items in the basket_, _Reviewing past orders and accounting_, etc.).

Anyway, I have witnessed in several occasions that the design of the _integration interfaces_ (eg. REST APIs, gRPC services, GraphQL, etc.) is neglected, as if those interfaces were less important, while in fact they represent the way a component of an enterprise architecture communicates with another component.

A well-designed REST API provides an elegant and easy way to perform one or many mutations to the information (eg. _create_, _update_ or _delete_) or the query of the most valuable information (eg. _paginated queries_)

I have observed that the origin of this pathology can be many times tracked down to the lack of _service design_ knowledge from within the team producing the components (for example, the appointed _architect_ has no preparation on the theoretical elements), or from a lack of domain knowledge about the service to be provided, or ultimately by a too large bounded context assigned to the service (that tracks back to the lack of _service design_ knowledge).

## Standards at the Rescue of DevOps

![DevOps](/assets/img/drafts/devops-infinity.png)

In our current landscape of the IT industry (_all-in-all_ cross-cutting considered), the ownership and leadership of development processes, in the vast majority of cases, doesn't require anymore the screening for the knowledge of specific theoretical elements of software engineering, given the scarcity of resources in the market, but also given the need of _producing fast_ (_from MVP to MVP_), that produces _bastard effects_ in the adoption of authoritative standards, which are employed only partially or with little consideration of their benefits.

Considering the _integration interfaces_ artifacts, standards like [OpenAPI](https://www.openapis.org/) or [GraphQL](https://graphql.org/) are used to align the efforts of the IT industry segments producing services and tooling, to ease the collaboration, governance and overall experience: for example, .NET libraries like [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle.AspNetCore) help with the generation of OpenAPI documents describing a service set of operations, and applications like [AutoRest](http://azure.github.io/autorest/) can interpret that generated standard and produce Java, Python, .NET or JavaScript client libraries, that interested consumers can easily integrate in their projects.

In such a process, the team responsible of producing and operating a service can produce an _authentic_ version of the client libraries for the consumers, reducing or eliminating the risk of proliferation of insecure alternatives, produced sometimes with a non consistent design or a narrow scope.

Providers of services, like [Microsoft Azure](https://azure.com), include in their DevOps process the generation and publication of both the [standard specification](https://github.com/Azure/azure-rest-api-specs) of the services offered, and the generated _language-specific_ client libraries, to reduce or eliminate the risk of integration: in fact, the above mentioned _AutoRest_ application implementation was originated from this need.

## Consumer Scenarios

The contrary of the virtue process described above, as many of you will recognize being the real state of things within a typical organization, is that teams responsible of producing a service, which need the integration of other services (within or without the same organization), not finding available client libraries for that specific service, are then forced to manually produce them, typically focusing on the parts of the integrated service relevant to their business, and therefore hardly reusable by other teams.

This approach causes a proliferation of integrations, creating insecurity (_which library should I use?_), distracting time and efforts by teams external from the integrated service in the maintainance of those artifacts, rsulting in ternsions at several levels of the organization.