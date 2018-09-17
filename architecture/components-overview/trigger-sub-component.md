# Trigger Plugins

In order to provide additional flexibility and to support custom requirements of end-user's CI/CD architectures, SitecoreDXG is designed to support the implementation of _Triggers_ and _Completion Handlers_ as modular _plugins_ of the Generation Service. While triggers and completion handlers are loaded by and installed onto the SitecoreDXG Generation Service, they are actually designed to be "injected", modular implementations of a predefined structure that the Generation Service knows how to communicate with.

By default, SitecoreDXG ships with the **SitecoreDXG RabbitMQ Trigger** which is pre-configured as the default trigger of the Generation Service. The SitecoreDXG RabbitMQ Trigger satisfies the _trigger_ role by listening to the RabbitMQ message queues and executing generation with passed in serialized template architecture data from queued messages when found. It should be noted that the SitecoreDXG RabbitMQ Trigger that is included by default is designed to work with the SitecoreDXG RabbitMQ Middleman that is also included out of the box.

It should also be noted that SitecoreDXG includes an alternative trigger, the Expressjs Service Trigger, that can be optionally used as a replacement for the RabbitMQ Trigger. The ExpressJs trigger is more intended to serve a high-level example than a fully-functional trigger - a limited set of features are supported and the service itself has not been optimize to receive the potentially large JSON payloads that would be submitted when generating the documentation for larger, more complex solutions.

The following diagram shows the involvement of a trigger plugin and the SitecoreUML Service for Sitecore in the high-level communication between the main components of fully-functional SitecoreDXG ecosystem: 

![](/assets/SitecoreDXG_Components_TriggerSerializerCommunication.png)

As a side-note, it's worth mentioning that SitecoreDXG also includes an alternative trigger, the Expressjs Service Trigger, that can be optionally used as a replacement for the RabbitMQ Trigger. The ExpressJs trigger is more intended to serve a high-level example than a fully-functional trigger - a limited set of features are supported and the service itself has not been optimize to receive the potentially large JSON payloads that would be submitted when generating the documentation for larger, more complex solutions.

