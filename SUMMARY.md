# Summary

## Overview

* [Introduction](README.md)
* [Comparison with SitecoreUML](comparison-with-sitecoreuml.md)

## Getting Started

* [Installing SitecoreDXG](getting-started/installing-sitecoredxg.md)
  * [General Installation](getting-started/general-installation.md)
    * Install the SitecoreDXG Generation Service
    * Install RabbitMQ
    * Install the SitecoreUML Service for Sitecore
  * [Advanced Installation](getting-started/advanced-installation.md)
* [Using the Default RabbitMQ Middleman and Trigger](getting-started/using-the-default-rabbitmq-middleman-and-trigger.md)
* [Documentation Configuration Settings](getting-started/controlling-documentation-configuration-in-sitecore.md)

## Architecture

* [Architecture Overview](architecture/architecture-overview.md)
* [Roles](architecture/roles.md)
  * Serializer Role
  * Middleman Role
  * Trigger Role
  * [Generator Role](architecture/generator.md)
  * [Completion Handler Role](architecture/completion-handler-role.md)
  * [Role Combinations](architecture/role-combinations.md)
* [Components](architecture/components-overview.md)
  * SitecoreDXG Middleman
  * SitecoreUML Service for Sitecore
  * SitecoreDXG Generation Service
    * Trigger Sub-component
    * Completion Handler Sub-component
  * Understanding the Default RabbitMQ Middleman and Trigger

## How To

* [CI/CD](how-to/cicd.md)
  * Integrating the default RabbitMQ Middleman
* Creating a Custom Trigger
* Creating a Custom Middleman
* Creating a Custom Completion Handler

