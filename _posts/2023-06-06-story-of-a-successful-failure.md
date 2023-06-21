---
layout: single
title: Story of a Successful Failure
date: 2023-06-06 20:40:40 +0200
categories: [startup]
tags: [architecture, startup, development, business, failure, success]
excerpt: "Sometimes we succeed to fail, doing something we love, following the white rabbit of passion into a deep hole of bad choices"
---

![Startup](/assets/img/2023-06-06-story-of-a-successful-failure/light-bulb-ideas-creative-diagram-concept.png)

As you can read from my [profile](/about), aside from my regular job as _Enterprise Architect_, during my free time I'm a software developer, and I love to create new things, to solve problems: as much as possible, I try to follow the _Lean Startup_ approach, to validate my ideas, and to create a _minimum viable product_ (MVP), eventually trying to scale it to start a business.

A couple of years ago, using the knowledge acquired during my time as architect in a telecommunication company, I decided to create a messaging platform to offer new way to send and receive A2P (_Application-to-Person_) messages, unifying different types of channels (_email_, _SMS_, _push notifications_, _Telegram_, _WhatsApp_, etc.) through a single API: a platform named _Deveel OCM_ (_Omni-Channel Messaging_).

I will not go in details here about the idea, the overall architecture, or its whole implementation, also because I believe that the majority of the project's idea, architecture and code was positive: I will rather share with you the story of how it failed, in a way that some might use as a _cautionary tale_, or as a way to learn from my mistakes (a sort of public _[post-mortem analysis](https://en.wikipedia.org/wiki/Postmortem_documentation)_).

Some of you will recognize some of your own stories in this one, but some others (maybe the majority) will read it and think _"I would never do such rookie mistakes"_: that is something I thought myself when reading similar stories posted by others, and given my training as developer, project manager and architect, but I eventually did those mistakes anyway, once mixing all roles together, and losing my objectivity.

## The Easy Part: A Working Proof-of-Concept

In fact, to rapidly validate the business idea, I diligently followed the good _lean practices_ that I observed in previous cases, and that I preach myself to developers and business owners: starting an _[innovation process](https://antonello.provenza.no/architecture/products/pace-layered-framework/)_ of my own, I developed a _monolithic_ application, aggregating together several sub-domains and entities (eg. _channels_, _terminals_, _webhooks_, _messages_, etc.) into one single service, cutting off architectural and code complexity, and speeding up the development time: in roughly two months I had developed the first version of a cloud-native messaging system, a notification service to deliver _webhook callbacks_ to subscribers (for incoming messages or event notifications), and a set of background services and infrastructure to run the majority of the features of the system (eg. _creating channels_, _creating terminals_, _sending messages to providers_, _receiving messages_, _retries_, _notifications_, etc.).

Although I didn't spend much time in the full design of the architecture, an agile project management process was in place (using _Kanban_ boards linked to code), and I did some domain analysis, defining _entities_, _events_, _services_, sensing the future complexity of the system and the opportunity to scale the platform, while being confident that the architecture was good enough to start with a demo.

## The Follow-Up: A Working MVP

![Software Development](/assets/img/2023-06-06-story-of-a-successful-failure/software-developer-programming-from-home.jpg)

Having achieved a working set of minimal features, I proceeded with demoing the system to some friends and colleagues, gaining some attention and a young business partner: this made me decide to go further, and to create a _Minimum Viable Product_ (MVP), to test the idea with real users, and possibly to start a business behind it.

To enable such scenario, I had to fill the gap of some missing services and components, such as an _administration portal_ (for users to manage their resources), a _registration service_, _authentications_ and _authorizations_, and a way to track the usage of the platform, and to provide insights to the users about the usage of the messaging (_analytics_).

This also meant scaling up the technical capabilities of some of the existing components, and to start thinking about the _infrastructure_ and the _deployment_ of the platform.

Fortunately, after reaching out to [Microsoft](https://microsoft.com), we were granted access to the [Startup Program](https://www.microsoft.com/en-us/startups), receiving a _Sponsored Subscription_ to the [Azure](https://azure.com) cloud platform, and other valuable perks: at the time I felt that was a great help and support, because I could focus on the development, and I didn't have to worry about the infrastructure, and the costs (after a couple of very expensive invoices for the usage of the platform in a development phase).

Anyway, for how much I appreciated and felt relieved by Microsoft support at that time, I realize now that it also might have been an issue for me, since I stopped feeling the _urgency_ of raising up funds to pay for the infrastructure, leading me to _relax_ and to start focusing on the architecture redesign towards an _ideal target state_ of the technology, rather than focusing on the _business_ development.

### The (Premature) Re-Architecture

Being an architect after all, I could not resist the temptation of applying _proper_ design principles and patterns, and thus I started breaking the monolith in several microservices, creating a complex and _distributed architecture_: that also had the consequence of re-designing the CI/CD pipelines to support a _distributed deployment_ model: not a small detail, given that each domain ended up having its own services, infrastructure, codebase.

Such an architecture was indeed implementing best practices, suited for large organizations, with multiple teams collaborating on the same system, and that need to scale up their agile development.

Anyway, I am not a large organization, and this approach failed me.

In fact, every fix, every change, every new feature, required me to work on several repositories, to restore dependencies and to update several configuration files: the time spent to implement, test and validate the changes multiplied by a factor of nine, and I was not able to keep up with the pace of the business idea I wanted to implement.

Design and architecture are the most important activities in the system development process: considering aspects such as _security_, _compliance_ (to regulations), _scalability_, _business continuity_, _DevSecOps_ is crucial for an established organization that produces software service solutions, but **it has to come at the right time** of the lifecycle, with the right scale of efforts in the right phase: I can easily say I failed myself evaluating at which stage I was myself (as a _one-man-startup_), starting a process of re-engineering that was premature and not needed.

### Filling the Gaps

As mentioned above, the initial _Proof-of-Concept_ of the system was intentionally and knowingly missing some key components, that were anyway required to make it to be usable by real users:

1. **Multi-Tenancy**: given the _Software-as-a-Service_ (SaaS) nature of the idea, the system lacked the capability to isolate resources, users and applications for specific tenants (organizations or individuals who would use the platform)
2. **Security**: the system lacked the security features to authenticate and authorize users and client applications
3. **Analytics**: the platform was missing a way to track the usage of the platform _entities_ (eg. _channels_, _terminals_, _message statuses_, _campaigns_, etc.), and to provide insights to the users about their usage
4. **Registration and Provisioning**: the platform lacked a service or process to onboard tenants and users, and the provisioning of an initial set of credentials and resources to use the platform
5. **Administration Portal**: potential users of the platform lacked a graphical interface to manage their resources, to configure the platform, create new applications and users for their tenants, reviewing the usage of the platform, etc.

As understandable, the above _enablers_ are not in fact part of the core _messaging_ domain, but rather sit aside as supporting capabilities and services, and as such I wanted to avoid _reinventing the wheel_, but rather trying to find vendors (that I could afford!) delivering such functions as _Software-as-a-Service_ (SaaS) themselves (without the complexity of installing and managing the software parts), so that I could focus on the core domain.

#### The Multi-Tenancy Issue

Although multi-tenancy is a pretty known model and architecture, it's not easy to implement, and it actually posed the greatest challenge to the initiative:

1. Vendors providing a multi-tenant authentication services are not affordable for a startup, this also includes the usage of _Azure Active Directory_ (that had limitations in the _Sponsored Subscription_ provided to us by Microsoft)
2. Resources must be all segregated for a specific tenant, isolating databases, logs, analytics
3. Access control must be enforced to a new level of granularity, since users and applications of a tenant must be able to access only their resources, and not the ones of other users or tenants

Not wishing to handle databases of secrets and credentials, to avoid any compliance issues, I initially discarded the usage of [Duende's IdentityServer](https://duendesoftware.com/products/identityserver), that anyway would have been a great fit for the system in later stage of maturity, but that also meant an additional service to handle my own, and I started looking for a _SaaS_ solution for the authentication and authorization of users and applications, delaying the decision to eventually switch to _IdentityServer_ in a later moment.

Playing safe, I resolved the issue of _missing authentication_ by using an instance of [Auth0](https://auth0.com), integrating the service through their _Management API_, that allowed me to provide some more _metadata_ to the user profiles, to logically group them in the context of tenants: this stole some time, since I could not use a plain _out-of-the-box_ registration process provided by Auth0 itself, given I needed users to carry the tenant identity since the start of their lifecycle within the platform.

Furthermore, Auth0 provides a very limited number of applications in its _free tier_ offering (although even in its _Enterprise tier_ the number of applications would have not been enough): because the _SaaS_ nature of the the system, the main consumers of the messaging functions were intended to be applications accessing the APIs, and users should have had the possibility to create one or many client applications per tenant, that meant having an unpredictable number of applications to authenticate.

This limitation _forced_ me to implement a custom solution to handle the creation of applications, to manage their credentials in a secure way, forking _application authentication_ and _user authentication_ processes.

For addressing the segregation of resources like _channels_, _terminals_, _messages_, I ended up relying on some _off-the-shelf_ .NET libraries provided from the community (for example, [Finbuckle.MultiTenant Library](https://www.finbuckle.com/multitenant)), especially for the discovery of the tenants and resolving their resources, although most of the complexity of the multi-tenant architecture I had to cover myself.

**Note to the Readers** - Implementing a _multi-tenant strategy_ requires more than just a library: it requires a _design_ of the architecture, and a _design_ of the data model, that is not easy to do, and that requires a lot of time, and a lot of testing (to ensure the resource segregation and availability).

#### The Analytics Service

Providing a messaging platform to users without the ability to review the performances of the resources they are using is not highly valuable, and thus I decided to implement an _Analytics Service_ to address this concern.

The implementation of such a service was another big challenge, since it required a large amount of data to be collected, stored and processed: I had to study the best way to execute on the processes, and provide the insights to the users on several dimensions, with the possibility to customize such reports. Although the number of performance indicators for analysis might scale to a large amount, I wanted to start small, and only considering the statuses of messages (eg. _queued_, _sent_, _delivered_, _failed_, etc.), also to avoid too many integration pipelines.

For the first version of this service I heavily relied on an instance of [ElasticSearch-as-a-Service](https://www.elastic.co/cloud/elastic-cloud) by [Elastic](https://elastic.co), but the costs rapidly scaled up to a point unbearable for me, and I had to find a cheaper solution, leveraging the resources available from within the _Azure Subscription_ I received as part of the _Microsoft Startup Program_: although services such as _[Azure Synapse](https://azure.microsoft.com/en-us/products/synapse-analytics/)_ were more suited than ElasticSearch to provide analytics, going from a model based on a search engine (that evaluates aggregated data _on-the-fly_) and a simple ingestion, to a model based on _staging_, _pipelines_, _data lakes_ and _data warehouse_ to produce specific type of analysis, required a lot of time and steep learning curve to migrate the service.

Although ultimately I succeeded, these tasks distracted me from the development of the MVP, and from the development of the platform itself, before any customer was even acquired, sacrificing the implementation of new channels to focus on this accessory service.

#### Registration and Provisioning Orchestration

_Authentication_, _Authorization_ and _Resources_ are not synonyms and consist of different processes, implement different models, and require dedicated components.

The onboarding process of a new user into the platform requires a set of coordinated movements between few services, especially in a distributed architecture, like the one I ended up implementing:

1. A unique (root) tenant has to be created to handle users, applications and resources (and potentially child tenants in the directory)
2. An administration (root) user must be created on the service that handles the authentication, within the context of the newly created tenant
3. A default set of resources (eg. databases, tables, file storages, etc.) must be created on each of the service that master a certain type of information, for the newly created tenant
4. The administration user must be granted access (through roles and direct grants) to the default set of resources and information
5. The identity of the user must be validated through a confirmation process (e-mails, sms, etc.) and activated

You might logically argue that large parts of the above process might have been provided _out-of-the-box_ by the Identity Management service, but as described above the requirement of a multi-tenant model and its lack of support by Auth0, I had to implement some _patches_ since the registration phase, forcing me to proxy the process through a custom service.

Furthermore, the coordination of creation of resources, including failures and retries, required a central service to handle the process, and to provide a _single point of failure_ for the process itself.

#### The Administration Portal

The last missing piece of the puzzle was the _Administration Portal_, to enable users to the management of their tenants, applications, resources, reviewing the analytics, etc.

Since I am not by inclination a _front-end_ developer, and not having formed a technical team where one could have taken responsibility of that interface, I had to study a way to implement a web application that could have fulfilled the scope, although just minimally, at the startup phase of the initiative (with the goal of replacing it later): I then opted for the implementation of a [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor) application, given its model, that provides a way to implement a web application using the same language and framework of the backend services, that meant I could skip learning specific JavaScript frameworks, _fighting_ with CSS, and focus on the implementation of the application itself.

Despite being an easy-to-use technology, it still took me some time to learn it, and several cycles to implement even the little changes required to the UI, and to the UX, and to make it usable by the users.

**Remember**: No matter how easy a technology is, the development of a graphical interface is one of the most time-consuming tasks, and requires a lot of iterations, and a lot of testing, to ensure that the user experience is good enough.

### The Experimentation Trap

As I mentioned above, being granted by Microsoft with a _Startup Program_ subscription relieved me from the urgency of finding revenues to support the infrastructure, and this brought me to a situation where I took a lot of liberty in the experimentation of new (at least for me) technologies and methodologies: it definitively benefitted my personal knowledge, but it also distracted me from the development of the platform itself, and from the acquisition of customers.

#### Microservices Alternatives

When I decided to break the monolithic architecture of the first service, I had to decide which technology to use to implement the new set of modules emerging from such choice, going through a long phase of _Proof-of-Concepts_ and _Proof-of-Technologies_.

Given the trends of the industry, I decided to try with [Kubernetes](https://kubernetes.io) and [Docker](https://www.docker.com), and to implement the services as _containers_, but I soon realized that the learning curve was too steep, and the complexity of the technology too high, to be able to implement it in a reasonable amount of time, and to be able to maintain it in the long term.

Wanting to keep the idea of using containers through an orchestrator, I then tried to benefit from the Microsoft's experimental [Project Tye](https://github.com/dotnet/tye), that offered a simple design to configure the cluster infrastructure, and to deploy the services: that succeeded for a while.

Since the overall set of components (databases, monitors, networks, secrets, API gateway, etc.) were resident in Azure, and the scope of the cluster was to host only the services, I was immediately posed the challenge of accessing external services from within the cluster (eg. _Azure Key Vault_, _Azure SQL Server_, _CosmosDB_, etc.) and to make the services reachable from the outside (eg. _Azure API Management_, _Azure Application Gateway_, etc.): for this I tried to use functions provided by the _[Dapr](https://dapr.io)k, but without much success.

After few attempts and iterations, leveraging the power of _Infrastructure-as-Code_ (_IaC_), I ended up with a set of _[Terraform](https://www.terraform.io)_ modules that were able to provision the services as _Azure Apps_ and _Azure Functions_, and to deploy the services, delegating the complexity of resource balancing to Azure, to eventually resume the possibility of using an orchestrator in the future: this choice brought benefits to the speed, costs and simplicity of the deployment, although it came after few iterations, and after a lot of time spent in the experimentation of new technologies.

#### Experimenting With Code

Overall the various changes and new implementations described above, the major mistake that I can identify was the choice of experimenting new methodologies for writing the source code of the services, leading to a lot of time spent in the implementation of more than one _code framework_ to reduce the amount of code to write, and to increase the speed of development.

As much as such practice is beneficial in the long term, it can also be a trap in the short time, since the .NET runtimes release new features quite quickly, that means I had spent a considerable amount of time _filling the gaps_ of missing features in the framework, to use the new features of the runtimes.

One of the most disappointing examples that describes this situation, was the implementation of a set of features to reduce the amount of time to log operations and events, optimizing the performances of such calls, to then receiving these same provisions from the version 7.0 of the .NET framework.

## The End of the Journey: The Shutdown

![Close](/assets/img/2023-06-06-story-of-a-successful-failure/we-are-closed-wooden-sign.png)

After a year of development, and after a year trying to find customers or partners (without success), I decided to shutdown the platform, and to stop the development, to avoid entering in the situation of having to pay for the infrastructure from my own pocket, without having any revenue in sight.

Some results were achieved, but not enough to justify the continuation of the project, and the costs of the infrastructure by myself, that without the support of the _Startup Program_ would have been not even closely affordable.

Along the way I learnt a lot about several aspects of the messaging domain, the underlying models and technologies, the challenges of implementing a _Software-as-a-Service_ platform (as developer), and the challenges of running a startup, although the failure of the project was disappointing nonetheless.

I don't exclude the possibility of reboot it later on, reusing the good parts (software libraries, applications, services) and lessons learnt along the way, but for the moment I am just focusing on absorbing the various technical, architectural and business lessons learnt, and on applying them to my current job.

## The Lessons Learnt

![Lessons Learnt](/assets/img/2023-06-06-story-of-a-successful-failure/learn-wooden-cubes.png)

They say that _if you don't learn from your mistakes, you are doomed to repeat them_, and I don't want to repeat the same mistakes again, leaving room for a bunch of new mistakes to do. 

As much as possible I would like that those of you who have read this post until now will benefit from the lessons I have learnt along this year:

1. **Avoid Scaling the Architecture Prematurely** - The decision to make the system too complex (through _micro-servicing patterns_) ahead of time was a mistake, that led to a lot of time spent on the architecture design, the infrastructure management, the dependency resolution, and other secondary concerns, rather than on the business logic, and on the business value
2. **Best Practices can be Misleading (Sometimes)** - The refactoring of the existing components to implement the missing _best practices_ and code patterns was a mistake that stolen a lot of valuable time: the code was good enough, secure enough, and performant enough to be productive (even after the re-architecture of the platform), and the changes were not required; furthermore such _best practices_ are opinionated and debated by the development community, making them not _an absolute truth_.
3. **Not Focusing on the Business Value** - The decision to focus on the _technical_ aspects of the platform, rather than on the _business_ aspects of the platform was a mistake, distracting me from the delivery of features and components that would have enabled the acquisition of customers
4. **Don't Work Alone** - One of the worst mistakes anyway was the decision to work alone on the implementation, without any technical partner in the development, someone with whom I could have shared the workload, receive an provide a different perspective on the development: although one might be expert enough to cover several aspects of a system (e.g. _infrastructure_, _analytics_, _messaging_, etc.), the time to allocate for each of the items to implement and manage will sum up and eat up the available capacity of the person.
