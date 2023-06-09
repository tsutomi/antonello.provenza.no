---
layout: single
title: Story of a Successful Failure
date: 2023-06-06 20:40:40 +0200
categories: [startup]
tags: [architecture, startup, development, business, failure, success]
excerpt: "Sometimes we succeed to fail, doing something we love, following the white rabbit of passion"
---

![Startup](/assets/img/2023-06-06-story-of-a-successful-failure/light-bulb-ideas-creative-diagram-concept.png)

As you can read from my [profile](/about/), aside from my regular job as _Enterprise Architect_, during my free time I'm a software developer, and I love to create new things, to solve problems: as much as possible, I try to follow the _Lean Startup_ approach, to validate my ideas, and to create a _minimum viable product_ (MVP), eventually trying to scale it to start a business.

A couple of years ago, using the knowledge acquired during my time as architect in a telecommunication company, I decided to create a messaging platform to offer new way to send and receive A2P (_Application-to-Person_) messages, unifying different types of channels (_email_, _SMS_, _push notifications_, _Telegram_, _WhatsApp_, etc.) through a single API: a platform named _Deveel OCM_ (_Omni-Channel Messaging_).

I will not go in details here about the idea, the overall architecture, or its whole implementation, also because I believe that the majority of the project's idea, architecture and code was positive, but rather share with you the story of how it failed, in a way that some might use as a _cautionary tale_, or as a way to learn from my mistakes.

Some of you will recognize yourself and your story in it, some others will read and think _"I will never do such rookie mistakes"_, that is something I thaught myself when observing similar stories by others.

## The Easy Part: A Working Proof-of-Concept

In fact, to rapidly validate the idea, I diligently followed the good _lean practices_ that I observed in previous cases, and that I preach myself to developers and business owners: starting an _innovation process_, I developed a _monolithic_ application, aggregating together several sub-domains and entities (eg. _channels_, _terminals_, _webhooks_, _messages_, etc.) into one single service, cutting off complexity, layers, and speeding up the development: in roughly two months time I had developed the first version of a cloud-native messaging system, exposed through a set of public REST APIs, a notification service to deliver _webhook callbacks_ to subscribers (for incoming messages or event notifications), and a set of background services and infrastructure to run the majority of the features of the system (eg. _creating channels_, _creating terminals_, _sending messages_, _retries_, _notifications_, etc.).

Although I didn't spend much time in the full design of the architecture, I did some domain analysis, defining _entities_, _events_, _services_, sensing the future complexity and the opportunity to scale the platform, while being confident that the architecture was good enough to start with a demo.

## The Follow-Up: A Working MVP

![Software Development](/assets/img/2023-06-06-story-of-a-successful-failure/software-developer-programming-from-home.jpg)

Having achieved a working set of minimal features, I proceeded with demoing the system to some friends and colleagues, gaining some attention and a partner (who had to focus on the business development): this made me decide to go further, and to create a _Minimum Viable Product_ (MVP), to test the idea with real users, and possibly to start a business behind it.

To enable such scenario, some missing services and components were missing, such as an _administration portal_, a _registration service_, _authentications_ and _authorizations_, and a way to track the usage of the platform, and to provide insights to the users about the usage of the messaging (_analytics_).

This also meant scaling up some of the existing components, and to start thinking about the _infrastructure_ and the _deployment_ of the platform, and to start thinking about the _business model_.

Fortunately, after reaching out to [Microsoft](https://microsoft.com), I was granted access to the [Startup Program](https://www.microsoft.com/en-us/startups), receiving a _Sponsored Subscription_ to [Azure](https://azure.com), and other valuable perks: at the time I felt that that was a great help from their side, because I could focus on the development, and I didn't have to worry about the infrastructure, and the costs.

Anyway, for how much I appreciated and felt relieved by Microsoft support at that time, I realize now that it also might have been an issue for me, since I stopped feeling the _urgency_ of raising up funds to pay for the infrastructure, leading me to _relax_ and starting focusing on the architecture redesign towards an _ideal target state_ of the technology, rather than focusing on the _business_ development.

## The (Premature) Re-Architecture

Being an architect after all, I could not resist the tentation of applying _proper design_ principles and patterns, and thus I started breaking the monolith in several microservices, creating a complex and _distributed architecture_, that also meant to design a _distributed deployment_: not a small detail, given that each domain ended up having its own services, infrastructure, codebase, CI/CD pipeline.

Such an architecture was indeed implementing best practices, suited for large organizations, with multiple teams collaborating on the same system, and that need to scale up their agile development. 

Anyway, I am not a large organization, and this approach failed me.

Every fix, every change, every new feature, required me to change several repositories, to restore dependencies and to update several configuration files: I was spending more time in _maintenance_ than in _development_, and I was not able to keep up with the pace of the business idea I wanted to implement.

Architectural thinking, design and implementation is one of the most important set of processes in the system development process: considering aspects such as _security_, _compliance_ (to regulations), _scalability_, _business continuity_, _DevSecOps_ is crucial for an established organization that produces software service solutions, but it has to come at the right time of the lifecycle, and here is where I failed myself evaluating at which stage I was myself (as a startup).

### Filling the Gaps

As mentioned above, the initial _Proof-of-Concept_ of the system was intentionally and knowingly missing some key components, that would have been required to make it to be usable by real users:

1. **Multi-Tenancy**: given the _Software-as-a-Service_ (SaaS) nature of the system, resources, users and applications had to be isolated from each other, and the system itself had to be able to scale up to support multiple tenants
2. **Security**: the system lacked the security features to authenticate and authorize users and client applications
3. **Analytics**: the platform was missing a way to track the usage of the platform _entities_ (eg. _channels_, _terminals_, _message statuses_, _campaigns_, etc.), and to provide insights to the users about their usage
4. **Registration and Provisioning**: none registration service or process to onboard tenants and users, and the provisioning of an initial set of credentials and resources to use the platform was not present
5. **Administration Portal**: potential users of the platform needed a way to manage their resources, and to configure the platform, create new applications and users for their tenants.

#### The Multi-Tenancy Issue

The above _enablers_ were not in fact part of the core _messaging_ domain, but rather supporting services, and I had then to study a model to avoid _reinventing the wheel_, trying to find vendors (that I could afford!) who could deliver a _multi-tenant_ set of functions in those regards.

Although multi-tenancy is a pretty known model and architecture, it's not easy to implement:

1. Vendors providing a multi-tenant authentication services are not affordable for a startup, this also includes the usage of Azure Active Directory (limited in the _Sponsored Subscription_ provided)
2. Resources must be all segregated for a specific tenant, isolating databases, logs, analytics

Playing safe, I resolved the issue of missing authentication by implementating an intergration to [Auth0](https://auth0.com), that stole some time to do, since I could not use a plain _out-of-the-box_ registration process, since I needed users to carry the tenant identity since the start of their lifecycle.

Furthermore, Auth0 provides a very limited number of applications in its _free tier_ offering (the one I was using), and since the scope of the system was to be consumed _programmatically_ through APIs (being a _SaaS_), giving to users the possibility to create one or many applications per tenant was an unavoidable requirement: this brought me to implement a custom solution to handle the creation of applications, and to store the credentials in a secure way, forking _application authentication_ and _user authentication_.

For addressing the segregation of the resources, I ended up relying on some _off-the-shelf_ .NET libraries provided from the community (for example, [Finbuckle.MultiTenant Library](https://www.finbuckle.com/multitenant)), especially for the discovery of the tenants and resolving their resources, although most of the complexity of the multi-tenant architecture I had to cover myself.

**Note to the Readers** - Implementing a _multi-tenant strategy_ requires more than just a library: it requires a _design_ of the architecture, and a _design_ of the data model, that is not easy to do, and that requires a lot of time, and a lot of testing (to ensure the resource segregation and availability).

#### The Analytics Service

Providing a platform to users without the ability to review the performances of the resources they are using results not highly valuable, and thus I decided to implement an _Analytics Service_ to track the usage of the platform, and to provide insights to the users about their usage.

Such a service was also a challenging component to implement, since it required a large amount of data to be collected, stored and processed: I had to study the best way to execute on the processes, and provide the insights to the users on several dimensions, with the possibility to customize such reports.

For the first implementation of this service I heavily relied on an instance of [ElasticSearch-as-a-Service](https://www.elastic.co/cloud/elastic-cloud) by [Elastic](https://elastic.co), but the costs rapidly scaled up to a point unbearable for me, and I had to find a cheaper solution, leveraging the resources available from within the _Azure Subscription_ I received as part of the _Microsoft Startup Program_: although such services were more suited than ElasticSearch to provide analytics, going from a model based on a search engine and a simple ingestion, to a model based on a _data warehouse_, _data pipelines_ and aggregations to produce specific type of analysis, and the transition required a lot of time for me to learn and migrate the service.

Although ultimately I succeded, these tasks distracted me from the development of the MVP, and from the development of the platform itself, before any customer was even acquired, acrificing the implementation of new channels to focus on this accessory service.

#### Registration and Provisioning Orchestration

_Authentication_, _Authorization_ and _Resources_ are not synonyms and consist of different processes, implement different models, and require dedicated components.

When onboarding a new user into the platform, a set of coordinated movements between few services is required, especially in a distributed architecture:

1. A unique (root) tenant has to be created to handle users, applications and resources (and eventually child tenants in the directory)
2. An administration (root) user must be created on the service that handles the authentication, within the scope of the newly created tenant
3. A default set of resources must be created on each of the service that handles the specific resources, within the scope of the tenant
4. The administration user must be granted access to the default set of resources (through roles and direct grants)
5. The identity of the user must be validated through a confirmation process (e-mails, sms, etc.)

You might logically argue that large parts of the above process might be provided _out-of-the-box_ by the authentication service, but since the service I was using was not designed for such a multi-tenant scenario, I had to implement some _patches_ since the registration phase, forcing me to proxy the process through a custom service.

#### The Administration Portal

The last missing piece of the puzzle was the _Administration Portal_, that was required to allow the users to manage their resources, and to configure the platform, create new applications and users for their tenants, reviewing the analytics, etc.

Since I am not natively a _front-end_ developer, I had to study a way to implement a web application that could have fulfilled the scope, although just minimally, at the beginning of the project: I then opted for the implementation of a [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor) application, and that was promising to allow the development of a web application using the same language and framework of the back-end services.

Despite being an easy-to-use technology, it still took me some time to learn it, and several cycles to implement even the little changes required to the UI, and to the UX, and to make it usable by the users.

## The End of the Journey: The Shutdown

After a year of development, and after a year of my partner trying to find customers or partners (without success), I decided to shutdown the platform, and to stop the development, to avoid entering in the situation of having to pay for the infrastructure from my own pocket, without having any revenue in sight.

Some results were achieved, but not enough to justify the continuation of the project, and the costs of the infrastructure by myself, that without the support of the _Startup Program_ would have been not even closely affordable.

Along the way I learnt a lot about several aspects of the messaging domain, the underlying models and technologies, the challenges of implementing a _Software-as-a-Service_ platform, and the challenges of running a startup, although the failure of the project was disappointing nonetheless.

I don't exclude the possibility of reboot it later on, reusing the good parts (software libraries, applications, services) and lessons learnt along the way, but for the moment I am just focusing on absorbing the various technical, architectural and business lessons learnt, and on applying them to my current job.

## The Lessons Learnt

They say that _if you don't learn from your mistakes, you are doomed to repeat them_, and I don't want to repeat the same mistakes again, and as much as possible I would like that those of you are reading this post will not make them either (a lot of space for doing new mistakes is still available).

1. **Over-Engineering the Architecture** - The decision to make the system too complex (through _micro-servicing patterns_) ahead of time was a mistake, that led to a lot of time spent on the architecture, and on the implementation of the architecture, rather than on the business logic, and on the business value
2. **Bad Practicing of Best Practices** - The re-implementation of the components to implement the missing _best practices_ and code patterns was a mistake that stolen a lot of valuable time: the code was good enough, secure enough, and performant enough to be productive (even after the re-architecting process), and the changes were not required, and furthermore opinionated and debated by the development community
3. **Not Focusing on the Business Value** - The decision to focus on the _technical_ aspects of the platform, rather than on the _business_ aspects of the platform was a mistake, that led to a lot of time spent on the technical aspects, rather than on the development of new features that would have enabled the acquisition of customers
4. **Don't Work Alone** - One of the worst mistakes was the decision to work alone on the implementation, without a partner in the development, who could have been able to share the workload, and to provide a different perspective on the development.