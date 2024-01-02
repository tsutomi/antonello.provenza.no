---
layout: single
title: Webhooks Activate Asynchronous Integration Patterns
categories: [open-source, events]
tags: [opensource, integration, webhooks, asynchronous, deveel]
excerpt: Activate the asynchronous integration patterns with webhooks is a common practice for service providers who wish to provide triggers and updates to their consumers.
lang: en
ref: webhooks-activate-asynchronous
---

In today's interconnected world, effective integration between various systems and services is crucial for the smooth operation of applications: _[Webhooks](https://en.wikipedia.org/wiki/Webhook)_ have emerged as a powerful mechanism for enabling real-time communication and event-driven architectures, enabling consuming applications to be triggered by events occurring in the service provider scope.

![Event Driven Architecture](/assets/img/2023-11-19-webhooks-activate-asynchronous/Event-Architecture.png)

In fact, a typical event-driven architecture uses highly performant messaging systems, generally deployed within the same network of the applications sending and receiving those kind of messages, also to reduce security and performance concerns. However, the typical use case of webhooks is to _export_ such event model outside the boundaries of a system or platform network.

## Domain Events and Integration Events

In the context of a distributed system, events can be classified into two main categories: _domain events_ and _integration events_.

Domain events are used to model events that occur within the boundaries of a single service or application: they are generally used to notify other components within the same system about changes in the state of the application. For example, a domain event might be triggered when a user places an order in an e-commerce application, or when a new customer is added to the database.

Integration events, on the other hand, are used to model events that occur between different services or applications: they are generally used to notify other systems about changes in the state of the application. For example, an integration event might be triggered when a user places an order in an e-commerce application, or when a new customer is added to the database.

## What are Webhooks?

Webhooks are a lightweight and flexible means of communication used to notify systems about specific _integration events_ or trigger actions: unlike traditional request-response mechanisms, webhooks follow the _publish-subscribe_ pattern, where a sender (known as the _webhook provider_) sends _HTTP POST_ requests to a specific URL (known as the _webhook endpoint_) when an event of interest occurs. The receiver (known as the _webhook consumer_) listens to these events and responds accordingly.

It is the responsibility of the _webhook provider_ to manage the subscriptions to certain events, and ensure that the _webhook consumer_ is notified when an event that matches the subscription occurs that same consumer is notified at the endpoint URL: this might involve several retries, and the _webhook provider_ should be able to handle errors and failures gracefully.

## How to Use Webhooks to Activate Asynchronous Designs

![Webhooks App Model](/assets/img/2023-11-19-webhooks-activate-asynchronous/Webhooks-App-Model.png)

Webhooks are an excellent tool for enabling asynchronous designs within an integrated architecture: by using webhooks, services can be decoupled, allowing them to communicate with each other without the need for synchronous _request-response_ interactions.

When an event occurs in a platform, the _webhook provider_ can notify all interested consumer applications simultaneously, enabling parallel processing and reducing latency.

A typical webhook payload, since its nature of _integration event_, also provides contextual information about entities and the occurrence, allowing the _webhook consumer_ to process it accordingly: for example, an e-commerce application might send a webhook notification when a customer places an order, including details such as the _order ID_, _customer name_, and _shipping address_. The _webhook consumer_ can then use this information to update its internal state and trigger other actions, such as sending an email confirmation or updating the inventory.

Webhooks allow systems to scale more effectively by handling events asynchronously. Following the example of the e-commerce application, when a customer places an order, the webhook provider can trigger an event that notifies the inventory management system, the payment gateway, and the shipping system simultaneously. Each system can independently process the event without waiting for the others, leading to improved performance and scalability.

## Deveel Webhooks

_[Deveel Webhooks](https://webhooks.deveel.org)_ is an open-source [.NET](https://dotnet.microsoft.com) framework that simplifies the implementation and handling of webhooks in .NET applications.

The framework is intended for someone who is looking to implement _*-as-a-Service_ (*aaS) solutions, where the service provider needs to expose webhooks to notify consumers about events occurring in the service. It provides a simple and intuitive API for configuring and managing webhooks, allowing you to focus on the business logic of your application rather than dealing with low-level HTTP interactions.

### Components of the Framework

The framework provides services at various levels of abstraction, allowing you to choose the level of control you need for your application:

* **Webhook Subscriptions**: the framework provides a generic interface for managing subscriptions to webhooks, allowing you to store them in a database or any other storage medium of your choice. It also provides a default implementation of the interface that uses a MongoDB database for storing subscriptions.
* **Webhook Notifications**: it also provides a generic interface for sending notifications to consumers that have subscribed to certain events, allowing you to implement your own webhook provider. It also provides a default implementation of the interface that uses the [ASP.NET Core HTTP Client](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/http-requests) for sending notifications.
* **Webhook Sender**: assuming you are willing to implement your own webhook subscription and notification services, or extending the default contracts, the framework provides a generic interface for sending notifications to consumers that have subscribed to certain events, allowing you to implement your own webhook provider.

### Using Deveel Webhooks in Your Applications

You can read more about how to use the framework in your applications in the [documentation](https://webhooks.deveel.org/getting-started), but the following example shows how to configure a webhook provider in your ASP.NET Core application, to start accepting subscriptions and notify consumers about events:

```csharp
public class Startup {
  public void ConfigureServices(IServiceCollection services) {
    services.AddWebhookSubscriptions<MongoWebhookSubscription>(options => {
      options.UseConnectionString("mongodb://localhost:27017");
    });

    services.AddWebhooksNotifier<MyWebhook>();
  }
}
```

The above example shows how to configure the framework to use a MongoDB database for storing subscriptions, and a custom webhook implementation for sending notifications to consumers: the framework provides a default implementation of the `IWebhook` interface, but you can also implement your own if you need to customize the behavior of the webhook provider.

This assumes that you are using the same instance of an ASP.NET Core application to implement both the webhook subscription management and the notification service: if you are using separate instances, you can use the `AddWebhookSubscriptions` method to configure the webhook provider in one application, and the `AddWebhooksNotifier` method to configure the webhook notifier in an second one, to obtain a better scalability of resources (suggested option).

### Event Transformations

In some scenarios you might need to transform the event payload before sending it to the consumer: for example, you might need to add additional information to the payload, or change the format of the data.

The framework provides a generic interface for implementing event transformations, allowing you to implement your own transformation logic, based on the type of event you are sending to the consumer.

**Note**: please consider that the above example refers to the current version of the framework (_v2.1.5_), and it might be subject to changes in the future: it is always recommended to refer to the [documentation](https://webhooks.deveel.org/) for the latest information, since at the time you are reading this post, the framework might have been updated.

Refer to the [GitHub repository of the framework](https://github.com/deveel/deveel.webhooks) for more information about the project, and how to contribute to it.

## Webhooks and CloudEvents

[CloudEvents](https://cloudevents.io/) is a specification for describing event data in a common format, making it easier to integrate systems that use different event formats. It provides a standardized way to express event metadata and payload, ensuring interoperability across various platforms and programming languages.

The main purpose and scope of use of CloudEvents is anyway still limited to the boundaries of a single network, and it doesn't provide any specification for the transport of events outside the boundaries of a system or platform network.

### Deveel Webhooks and CloudEvents

The [Deveel Webhooks](https://webhooks.deveel.org) framework doesn't provide any specific implementation of the CloudEvents specification, since it is intended to be used as a general-purpose framework for implementing webhooks in .NET applications: however, an outstanding feature request is to provide a CloudEvents implementation for the framework, to allow developers to use the framework in conjunction with other CloudEvents-compliant systems.
