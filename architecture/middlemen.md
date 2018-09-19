# Middlemen

In the SitecoreDXG ecosystem, the _middleman_ is responsible for retrieving the serialized data from Sitecore and forwarding it along to the SitecoreDXG Generation Service for generation.

Natively, middlemen are independent programs that run separately from the SitecoreDXG Generation Service, and the node-based [RabbitMQ Middleman](understanding-the-default-rabbitmq-middleman-and-trigger.md) is included by default. It is worth noting, however, that additional middlemen can be added at any time and can be written in PowerShell, C\#, Node.js, Java, Python, or any other language capable of calling the serializer \(via HTTP request, by default\) and passing the response to the trigger \(via RabbitMQ by default\). 

