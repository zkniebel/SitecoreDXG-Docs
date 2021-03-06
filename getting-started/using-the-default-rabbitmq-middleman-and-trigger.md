# Using the Default RabbitMQ Middleman and Trigger

The RabbitMQ Middleman can be found in the`.\middlemen\RabbitMQ\\`folder. Feel free to call the middleman directly from that folder or to copy that folder to another path or even another machine. If you do choose to move the file to another path or machine, be sure to run`npm init`to create a`package.json`file for it.

The RabbitMQ Middleman should be called using the following command-line syntax:

```
node rabbitmq-amqp-middleman CONNECTION_STRING ARCHITECURE_GET_URL GENERATION_QUEUE_NAME [COMPLETION_HANDLER_NAMES]
```

The middleman's parameters are as follows:

* `CONNECTION_STRING`**: **the RabbitMQ connection string to connect to
* `ARCHITECTURE_GET_URL`**: **the URL to get the serialized template architecture from
* `GENERATION_QUEUE_NAME`**: **the name of the generation queue to add the serialized response to
* `COMPLETION_HANDLER_NAMES`**: **\(optional\) a comma-separated string list of the names of the completion handlers that the Generation Server should call after generation completes

#### Examples

The following examples show how you can call the RabbitMQ middleman on a Habitat instance with the SitecoreUML Service \(1.3.6+\) installed:

_To retrieve the architecture and add the result to the documentation queue for generation..._

```
node rabbitmq-amqp-middleman amqp://localhost http://local.habitat.com/sitecoreuml/sitecoredxg/GetTemplateArchitecture "generation_queue__documentation"
```

_To retrieve the architecture and add the result to the metadata-json queue for generation..._

```
node rabbitmq-amqp-middleman amqp://localhost http://local.habitat.com/sitecoreuml/sitecoredxg/GetTemplateArchitecture "generation_queue__mdj"
```

_To retrieve the architecture and add the result to the documentation queue for generation and will tell the Generation Service to call a completion handler named "helloWorld" when finished..._

```
node rabbitmq-amqp-middleman amqp://localhost http://local.habitat.com/sitecoreuml/sitecoredxg/GetTemplateArchitecture "generation_queue__documentation" "helloWorld"
```

_To retrieve the architecture and add the result to the documentation queue for generation and will tell the Generation Service to call the "foo" and then the "bar" completion handlers when finished..._

```
node rabbitmq-amqp-middleman amqp://localhost http://local.habitat.com/sitecoreuml/sitecoredxg/GetTemplateArchitecture "generation_queue__documentation" "foo,bar"
```



