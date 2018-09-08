# Integrating the Default TeamCity RabbitMQ Meta-Runner

SitecoreDXG includes a TeamCity meta-runner that can be found in the same folder as the [RabbitMQ middleman](/getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger.md). You can integrate the meta-runner into your CI/CD process by doing the following:

1. Install the meta-runner on your TeamCity server by following the steps in the [TeamCity Meta-Runners documentation](https://confluence.jetbrains.com/display/TCD18/Working+with+Meta-Runner)
2. Copy the contents of the RabbitMQ middleman's folder \(excluding the TeamCity Meta-Runner definition XML file\) to your TeamCity build runner at a location that your runner will have permissions to access
3. In a browser, navigate to your TeamCity Web UI and add a new build step to the desired project
4. Select "SitecoreDXG RabbitMQ Middleman Runner" from the "Runner Type" drop-down and fill in the fields with the relevant details, following the help-text for each field. Be sure to set the _Script Path_ to the location where you copied the RabbitMQ middleman folder's contents in _step 2_
5. Run your build and confirm that the architecture was successfully added to the generation queue in the build log \(via checking that the correct number of bytes was sent to the queue\) 

![](/assets/SitecoreDXG-TeamCity-MetaRunner.png)

