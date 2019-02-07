# Integrating the Default TeamCity RabbitMQ Meta-Runner

SitecoreDXG includes a TeamCity meta-runner that can be found in the same folder as the [RabbitMQ middleman](../../getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger/). You can integrate the meta-runner into your CI/CD process by doing the following:

1. Install the meta-runner, `SitecoreDXGRabbitMQ_MiddlemanTeamCity_MetaRunner.xml`, on your TeamCity build server by following the steps in the [TeamCity Meta-Runners documentation](https://confluence.jetbrains.com/display/TCD18/Working+with+Meta-Runner#WorkingwithMeta-Runner-InstallingMeta-Runner)
2. [Install the default RabbitMQ Middleman](../../getting-started/installing-sitecoredxg/general-installation/optional-install-the-default-rabbitmq-middleman.md) \(excluding the TeamCity Meta-Runner definition XML file\) in a location that the build will have permissions to access \(e.g. on the build agent server\)
3. In a browser, navigate to your TeamCity Web UI and add a new build step to the desired build configuration
4. Select "SitecoreDXG RabbitMQ Middleman Runner" from the "Runner Type" drop-down and fill in the fields with the relevant details, following the help-text for each field. Be sure to set the _Script Path_ to the location where you copied the RabbitMQ middleman folder's contents in _step 2_
5. Run your build and confirm that the architecture was successfully added to the generation queue in the build log \(via checking that the correct number of bytes was sent to the queue\) 

