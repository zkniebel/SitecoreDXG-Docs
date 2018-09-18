# Compatibility & System Requirements

The following compatibility and system requirements must be satisfied in order to run SitecoreDXG.

## Sitecore Compatibility

Technically, SitecoreDXG integrates with the [SitecoreUML Service for Sitecore](/getting-started/general-installation/install-the-sitecoreuml-service-for-sitecore.md), rather than implementing directly with Sitecore itself. However, as SitecoreDXG is a member of the SitecoreUML family, this section describes its compatibility with the available Sitecore versions and deployment models.

### Versions

The below are the versions of Sitecore that SitecoreDXG is compatible with:

* Sitecore 7.2+ \(not tested with earlier versions, but may work\)
* Sitecore 8+
* Sitecore 9+

### Deployment Models

SitecoreDXG is compatible with the following Sitecore deployment models:

* **PaaS** \(Platform as a Service\)
* **IaaS** \(Infrastructure as a Service\)
* **On-Premises**

## System Requirements

This section describes the system requirements of SitecoreDXG infrastructure.

### SitecoreDXG Generation Service

The SitecoreDXG Generation Service requires the following minimum specifications:

* 1x CPU Core 2 GHz[^1]
* 2+ GB RAM[^2] \(8 GB recommended\)
* 1+ GB Storage[^3] \(20 GB recommended\)
* Windows[^4] \(any version supported by node.js\)
* Can be cloud-hosted via IaaS,

### SitecoreDXG RabbitMQ Middleman

The SitecoreDXG RabbitMQ Middleman requires the following minimum specifications:

* Any Windows, Linux or Mac OS supported by node.js \(tested with Windows only\)

### SitecoreDXG TeamCity RabbitMQ Middleman Runner

The SitecoreDXG TeamCity RabbitMQ Middleman Runner requires the following minimum specifications:

* Windows-based[^5] agent compatible with SitecoreDXG RabbitMQ Middleman

### RabbitMQ

In addition to the minimum specifications required by [RabbitMQ](https://www.rabbitmq.com/), the following minimum specifications must be met:

* Any deployment of RabbitMQ is supported, including on-premises, IaaS \(infrastructure as a service\) and SaaS \(software as a service; e.g. [CloudAMQP](https://www.cloudamqp.com/)\)



---

[^1]: Generation will be faster with a faster processor, but at present SitecoreDXG is only set up to use a single CPU core. Improvements are currently underway to change this.

[^2]: The generation service will use as much RAM as is available during generation, so the more RAM you have the faster the generation will be

[^3]: Depending on how you use SitecoreDXG you may want significantly more storage space than this. To install SitecoreDXG and start running it, you will need at least 1 GB, but unless you are deleting your output from the host machine after every generation then you will run out of storage space very quickly.

[^4]: Linux and Mac support is a planned addition for the future

[^5]: Linux and Mac support is a planned addition for the future

