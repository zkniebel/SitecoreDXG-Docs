# Step 2: Install RabbitMQ

The second step in the installation is to install RabbitMQ, keeping in mind that _**RabbitMQ can be installed on the same machine as other components, on its own dedicated machine, or it can be cloud hosted.**_

The below documentation assumes that you are installing RabbitMQ on a Windows machine, though you should be able to adapt these instructions to your desired deployment topology, as needed.

### Step 2a: Install RabbitMQ \(verified with 3.7.6+\)

Install RabbitMQ by following the [RabbitMQ installation documentation](https://www.rabbitmq.com/download.html).

Additionally, make sure that if you install RabbitMQ on a server that is reachable by the public domain that you [configure the necessary TLS/SSL settings](https://www.rabbitmq.com/ssl.html) to secure your message queues.

### Step 2b: Configure SitecoreDXG to Connect to RabbitMQ

Once you have finished configuring RabbitMQ you should have a working connection string, e.g.`"amqp://localhost"`. Be sure that you call the middleman with this connection string.

Next, add a heartbeat parameter to the connection string, e.g.`"amqp://localhost?heartbeat=60"`, and update your SitecoreDXG Generation Server's `./settings.js` file with the updated connection string value. The heartbeat parameter will help to keep the connection alive. Note that you do not need to call the Middleman with the heartbeat parameter.

Finally, after updating the settings, be sure to go into your Services manager \(type `services.msc` into the Windows _Start Menu_\), find the SitecoreDXG Generation Service in the list and restart it.

