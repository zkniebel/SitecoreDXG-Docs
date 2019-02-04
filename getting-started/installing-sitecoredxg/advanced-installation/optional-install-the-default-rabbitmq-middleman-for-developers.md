# 4. \(Optional\) Install the Default RabbitMQ Middleman for Developers

When installing SitecoreDXG you can choose to install the default RabbitMQ Middleman that is included with the product. If you choose to install the default RabbitMQ Middleman, keep in mind that _**the middleman does not have to be installed on the same machine as the RabbitMQ server, the SitecoreDXG Generation Service or the Sitecore instance. However, it may need to be on the same machine as your CI/CD server, depending on your use-case.**_

## Installation Location Freedom

You can install the RabbitMQ Middleman in the location of your choosing.

For example, if you plan to integrate SitecoreDXG into your CI/CD pipeline then you may wish to copy the RabbitMQ middleman to your CI/CD server. If you are using TeamCity, then you may wish to also install the [SitecoreDXG TeamCity Meta-Runner](../../../how-to/cicd/integrating-the-default-teamcity-rabbitmq-meta-runner.md) on your TeamCity server, for a seamless integration between TeamCity and the RabbitMQ middleman.

For more details on how the middleman chould be installed in a custom location and how it can be called from the command-line, see [Using the Default RabbitMQ Middleman and Trigger](../../using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger/).

## Installing the Default RabbitMQ Middleman

1. Download the [`SitecoreDXG-Dev-<version>.<build>.zip`](../../downloads.md) to your machine and extract in a location of your choosing. Note that it does not matter where you store it.
2. In the extracted directory, navigate to `./middlemen` and take note of the `./RabbitMQ` folder. This folder is your middleman's installation directory.
3. Copy the middleman's installation directory to the location of your choosing. 

