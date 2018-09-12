# Components

A _component_ is a modular program or service that is \(primarily\) independent of other programs or systems in/on which they are hosted, and satisfies the responsibilities of a SitecoreDXG _role_. By default, a fully-functional SitecoreDXG ecosystem includes the following components:

1. **SitecoreUML Service for Sitecore: **a service endpoint installed on a Sitecore application \(PaaS or non-PaaS\) as a Sitecore package that satisfies the _serializer_ role
2. **SitecoreDXG Middleman: **a program that satisfies the _serializer_ role - can be replaced with a own custom middleman implementation, though the **SitecoreDXG RabbitMQ Middleman **is included with SitecoreDXG for rapid setup and use
3. **SitecoreDXG Generation Service: **a node-based service \(installable as a Windows service\) that initializes and loads the _trigger_ and _completion handlers_ defined in the configuration, and satisfies the _generator_ role by performing the generation when called

The following diagram depicts how these components communicate at a high-level:

![](/assets/SitecoreDXG_Architecture__Components_Overview.png)

