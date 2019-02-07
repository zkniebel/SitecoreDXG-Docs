# CI/CD Integration

SitecoreDXG was specifically designed for ease of integration into any CI/CD pipeline. To integrate SitecoreDXG into your CI/CD pipeline refer to the following options, based on which platform you are using:

* **TeamCity -** SitecoreDXG includes a TeamCity build runner \(i.e. a SitecoreDXG Build Step type that you select from the "runner" drop down\) that will help to accelerate your setup. See [Integrating the Default TeamCity RabbitMQ Meta-Runner](integrating-the-default-teamcity-rabbitmq-meta-runner.md) page for details on how to get set up.
* **Other Platforms -** Remember that SitecoreDXG's execution flow is started by the middleman, and the included RabbitMQ middleman is CLI-driven. This means that you can integrate SitecoreDXG into your pipeline by adding a build-step to call your middleman from the command line. See [Integrating SitecoreDXG into your CI/CD Pipeline](integrating-sitecoredxg-into-your-ci-cd-pipeline.md) for more details, including setup instructions and a ready-to-use PowerShell script to call your middleman from a build step.

