# Completion Handler Sub-component

SitecoreDXG is meant to integrate easily with any CI/CD or end-user setup, which means that SitecoreDXG needs to support post-generation actions that should be run if the generation was successful. This is where _completion handlers_ come in. _Completion handlers_ run after a successful build and can be used to run any custom logic on the output that you want. They are designed to be the most easily extensible and replaceable entity in the SitecoreDXG ecosystem, so that you can make SitecoreDXG work for any use-case. 

SitecoreDXG ships with two working _completion handlers_, [AWS S3 Deploy](/getting-started/using-sitecoredxg/using-the-provided-aws-s3-deploy-completion-handler.md) and [Azure Blob Storage Deploy](/getting-started/using-sitecoredxg/using-the-provided-azure-blob-storage-deploy-completion-handler.md), that are ready for immediate use, as well as an example _completion handler_, [helloWorld.js](/how-to/creating-a-custom-completion-handler.md), to help those looking to create handlers for themselves.

Because completion handler logic is generally specific to the requirements of the end-user's CD/CD architecture, no handlers are configured to be called by default for SitecoreDXG, out of the box. In other words, while SitecoreDXG does include completion handlers for deploying to an AWS S3 bucket or an Azure Blob Storage container out of the box, using one or more completion handlers is entirely optional.

See [Creating a Custom Completion Handler](/how-to/creating-a-custom-completion-handler.md) for more details on the example and how to write your own completion handlers.

## How to Use a Completion Handlers

The most popular way to completion handlers is to specify the completion handlers that you want to use in the input payload of the serialized data that is passed from the middleman to the trigger. The [default RabbitMQ middleman](/getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger.md) supports passing the completion handler ID and necessary parameters as a CLI argument, and the [TeamCity Meta-Runner](/how-to/cicd/integrating-the-default-teamcity-rabbitmq-meta-runner.md) exposes a field for doing the same.

SitecoreDXG also supports the ability to set a default handler or set of handlers to run should no handlers be specified to run in in the input payload. You can set the default handler\(s\) in the `./settings.js` file of your SitecoreDXG Generation Service application.

## Completion Handler Examples

For some ideas/examples of completion handlers, have a look at the [Completion Handler Ideas](/how-to/creating-a-custom-completion-handler.md#completion-handler-ideas) section.

