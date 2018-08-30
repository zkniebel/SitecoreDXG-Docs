# Trigger Sub-component

In order to provide additional flexibility and to support custom requirements of end-user's CI/CD architectures, SitecoreDXG is designed to support the implementation of_Triggers_and_Completion Handlers_as modular_sub-components_of the Generation Service. While triggers and completion handlers are loaded by and installed onto the SitecoreDXG Generation Service, they are actually designed to be "injected", modular implementations of a predefined structure that the Generation Service knows how to communicate with.

By default, SitecoreDXG ships with and enables the**SitecoreDXG RabbitMQ Trigger**in the Generation Service to satisfy the_trigger_role by listening to the RabbitMQ message queues and executing generation with serialized template architecture data in queued messages when found. It should be noted that the SitecoreDXG RabbitMQ Trigger included by default is designed to work with the SitecoreDXG RabbitMQ Middleman that is also included. It should also be noted that SitecoreDXG includes an alternative trigger, the Expressjs Service Trigger, that can be optionally used as a replacement for the RabbitMQ Trigger. This trigger is meant more as a high-level example than anything else.

The following diagram shows the involvement of a trigger sub-component and the SitecoreUML Service for Sitecore in the high-level communication between the main components of fully-functional SitecoreDXG ecosystem:

...

