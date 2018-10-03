# Using SitecoreDXG

SitecoreDXG is meant to be a command-line-based, GUI-less tool that can be called manually from CLI or from an automated process, like a CI/CD pipeline.

In order to understand how SitecoreDXG works, it is suggested that you review the information in the _Architecture_ section before continuing. However, if you wish to get started quickly then the short version is that SitecoreDXG works by using a _middleman_ to retrieve the serialized data from Sitecore and kick off the generation process. At the end of the process, optional _completion handlers_ can be executed to "do something" with the generated output, or you can leave the generated output in the SitecoreDXG output directory for later review/use.

## Executing Generation

The execution flow should start by executing the default RabbitMQ Middleman, which will handle kicking off the rest of the process. See [Understanding the Default RabbitMQ Middleman and Trigger](../../architecture/understanding-the-default-rabbitmq-middleman-and-trigger.md) and [Using the Default RabbitMQ Middleman and Trigger](using-the-default-rabbitmq-middleman-and-trigger.md) for more details on the default middlemen included with SitecoreDXG, and see below for a high-level overview of the execution workflow.

## High-Level Execution Flow

At a high-level, the out of the box process works in the following way \(using the RabbitMQ middleman and trigger\):

1. Middleman runs \([executed from CLI or automated process](using-the-default-rabbitmq-middleman-and-trigger.md)\)
   1. Retrieves serialized data from SitecoreUML Service that is installed on the desired Sitecore instance
   2. Submits returned response to the desired RabbitMQ generation queue \(`generation_queue__documentation` for generating HTML documentation or `generation_queue__mdj` for generating just the Meta-Data JSON file\)
2. Trigger runs
   1. Trigger listens for messages added to the RabbitMQ generation queues
   2. Trigger detects a new message in one of the queues
   3. Trigger kicks off the generation action associated with the queue that the message was in and passes in the message contents
3. SitecoreDXG Generation Service executes generation
   1. Generated output is saved to an output folder
   2. Completion handlers are called based on specified handlers when generation was called or else the default settings of the Generation Service
4. \(Optional\) Completion handlers run
   1. Completion handlers run to do something with the generated output

