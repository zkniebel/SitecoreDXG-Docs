# CI/CD Integration

SitecoreDXG was specifically designed for integration into CI/CD pipelines. To integrate SitecoreDXG into your CI/CD pipeline, you can do one of the following:

* **Execute the provided RabbitMQ middleman**, which is a simple node script that supports the execution of any custom _completion handlers_ that you may have installed on your _SitecoreDXG Generation Service_. See [Integrating the Default RabbitMQ Middleman](/how-to/cicd/integrating-the-default-rabbitmq-middleman.md) for more.
* **Use the provided TeamCity meta-runner**, which is based on the provided RabbitMQ middleman, in order to easily add a SitecoreDXG generation build step to your TeamCity-based CI/CD pipeline. See [Integrating the Default TeamCity RabbitMQ Meta-Runner](/how-to/cicd/integrating-the-default-teamcity-rabbitmq-meta-runner.md) for more.



