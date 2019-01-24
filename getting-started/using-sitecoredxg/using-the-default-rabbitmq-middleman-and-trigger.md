# Using the Default RabbitMQ Middleman and Trigger

The RabbitMQ Middleman can be called from any location using the following command-line syntax:

```text
node rabbitmq-amqp-middleman CONNECTION_STRING ARCHITECURE_GET_URL GENERATION_QUEUE_NAME [OPTIONS]
```

The middleman's parameters are as follows:

* `CONNECTION_STRING`**:** the RabbitMQ connection string to connect to
* `ARCHITECTURE_GET_URL`**:** the URL to get the serialized template architecture from
* `GENERATION_QUEUE_NAME`**:** the name of the generation queue to add the serialized response to
* `OPTIONS`**:** \(optional\) JSON-formatted string object that can include a documentation configuration object property and/or completion handlers array of objects with the handler ID and parameters for each handler that should be used; Should have the following syntax: 

```text
'{\"DocumentationConfiguration\":{\"CommitAuthor\":\"ZacharyKniebel\",\"CommitHash\":\"0FE1D344\",\"CommitLink\":\"http://mygit.com/repo/myrepo/commits/0FE1D344\",\"DeployLink\":\"http://mydocs.com/foo/bar\"},\"CompletionHandlers\":[{\"ID\":\"MyHandler1\",\"Params\":{\"foo\":\"bar\"},{\"ID\":\"MyHandler2\"}]}'
```

## Examples <a id="examples"></a>

The following examples show how you can call the RabbitMQ middleman on a Habitat instance with the SitecoreUML Service \(1.3.6+\) installed:

_To retrieve the architecture and add the result to the documentation queue for generation..._

```text
node rabbitmq-amqp-middleman amqp://localhost http://local.habitat.com/sitecoreuml/sitecoredxg/GetTemplateArchitecture "generation_queue__documentation"
```

_To retrieve the architecture and add the result to the metadata-json queue for generation..._

```text
node rabbitmq-amqp-middleman amqp://localhost http://local.habitat.com/sitecoreuml/sitecoredxg/GetTemplateArchitecture "generation_queue__mdj"
```

_To retrieve the architecture and add the result to the documentation queue for generation and will tell the Generation Service to call a completion handler named "helloWorld" when finished..._

```text
node rabbitmq-amqp-middleman amqp://localhost http://local.habitat.com/sitecoreuml/sitecoredxg/GetTemplateArchitecture "generation_queue__documentation" '{\"CompletionHandlers\":[{\"ID\":\"helloWorld\"}]}'
```

_To retrieve the architecture and add the result to the documentation queue for generation and will tell the Generation Service to call the "MyHandler1" completion handler with parameters 1, 2, "foo", and "bar"; and then the "MyHandler2" completion handler with no parameters when finished..._

```text
node rabbitmq-amqp-middleman amqp://localhost http://local.habitat.com/sitecoreuml/sitecoredxg/GetTemplateArchitecture "generation_queue__documentation" '{\"CompletionHandlers\":[{\"ID\":\"MyHandler1\",\"Params\":[1,2,\"foo\",\"bar\"]},{\"ID\":\"MyHandler2\"}]}'
```

[    
](https://zkniebel.gitbooks.io/sitecoredxg/content/architecture/architecture-overview.html)

