# Using the Default RabbitMQ Middleman and Trigger

The RabbitMQ Middleman can be called from any location using the following command-line syntax:

```text
node rabbitmq-amqp-middleman CONNECTION_STRING ARCHITECURE_GET_URL GENERATION_QUEUE_NAME [OPTIONS_FILE_PATH]
```

The middleman's parameters are as follows:

* `CONNECTION_STRING`**:** the RabbitMQ connection string to connect to
* `ARCHITECTURE_GET_URL`**:** the URL to get the serialized template architecture from
* `GENERATION_QUEUE_NAME`**:** the name of the generation queue to add the serialized response to
* `OPTIONS_FILE_PATH`**:** \(optional\) Path to a JSON file that contains an object that may include a documentation configuration object property and/or completion handlers array property with objects representing the handler ID and parameters for each handler that should be used; For example: 

{% code-tabs %}
{% code-tabs-item title="SampleOptions.json" %}
```javascript
{
    "DocumentationConfiguration": {
        "CommitAuthor": "Zachary Kniebel",
        "CommitHash": "0FE1D344",
        "CommitLink": "http://mygit.com/repo/myrepo/commits/0FE1D344",
        "DeployLink": "http://mydocs.com/foo/bar"
    },
    "CompletionHandlers": [
        {
            "ID": "MyHandler1",
            "Params": {
                "foo": "bar"
            }
        },
        {
            "ID": "MyHandler2"
        }
    ]
} 
```
{% endcode-tabs-item %}
{% endcode-tabs %}

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

{% code-tabs %}
{% code-tabs-item title="hello-world-sample.json" %}
```javascript
{"CompletionHandlers":[
    {
        "ID":"helloWorld"
    }]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```text
node rabbitmq-amqp-middleman amqp://localhost http://local.habitat.com/sitecoreuml/sitecoredxg/GetTemplateArchitecture "generation_queue__documentation" "./hello-world-sample.json"
```

_To retrieve the architecture and add the result to the documentation queue for generation and will tell the Generation Service to call the "MyHandler1" completion handler with a parameters object; and then the "MyHandler2" completion handler with no parameters when finished..._

{% code-tabs %}
{% code-tabs-item title="handlers-1-2-sample.json" %}
```javascript
{
    "CompletionHandlers": [
        {
            "ID": "MyHandler1",
            "Params": {
                "Count": 1,
                "Max": 2,
                "Hello": "world!",
                "Foo": [ "bar", "baz", 12345 ]
            }
        },
        {
            "ID": "MyHandler2"
        }
    ]
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

```text
node rabbitmq-amqp-middleman amqp://localhost http://local.habitat.com/sitecoreuml/sitecoredxg/GetTemplateArchitecture "generation_queue__documentation" "./handlers-1-2-sample.json"
```

[    
](https://zkniebel.gitbooks.io/sitecoredxg/content/architecture/architecture-overview.html)

