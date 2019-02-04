# Table of contents

* [SitecoreDXG: The Documentation Experience Generator](README.md)

## Overview

* [SitecoreDXG: The Documentation Experience Generator](overview/overview.md)
* [Comparison with SitecoreUML](overview/comparison-with-sitecoreuml.md)
* [CI/CD Integration](overview/ci-cd-integration.md)
* [Helix Dependency Validation](overview/helix-validation.md)

## Getting Started

* [Compatibility and System Requirements](getting-started/compatibility-and-system-requirements.md)
* [Installing SitecoreDXG](getting-started/installing-sitecoredxg/README.md)
  * [General Installation](getting-started/installing-sitecoredxg/general-installation/README.md)
    * [1. Install the SitecoreDXG Generation Service](getting-started/installing-sitecoredxg/general-installation/install-the-sitecoredxg-generation-service.md)
    * [2. Install RabbitMQ](getting-started/installing-sitecoredxg/general-installation/install-rabbitmq.md)
    * [3. Install the SitecoreUML Service for Sitecore](getting-started/installing-sitecoredxg/general-installation/install-the-sitecoreuml-service-for-sitecore.md)
    * [4. \(Optional\) Configure the Documentation Configuration Item for your Solution](getting-started/installing-sitecoredxg/general-installation/optional-configure-the-documentation-configuration-item-for-your-solution.md)
    * [5. \(Optional\) Install the Default RabbitMQ Middleman in a Custom Location](getting-started/installing-sitecoredxg/general-installation/optional-install-the-default-rabbitmq-middleman.md)
  * [Developer Installation](getting-started/installing-sitecoredxg/advanced-installation/README.md)
    * [1. Install the SitecoreDXG Generation Service for Developers](getting-started/installing-sitecoredxg/advanced-installation/install-the-sitecoredxg-generation-service-for-developers.md)
    * [2. Install RabbitMQ for Developers](getting-started/installing-sitecoredxg/advanced-installation/install-rabbitmq-for-developers.md)
    * [3. Install the SitecoreUML Service for Sitecore for Developers](getting-started/installing-sitecoredxg/advanced-installation/install-the-sitecoreuml-service-for-sitecore-for-developers.md)
    * [4. \(Optional\) Install the Default RabbitMQ Middleman for Developers](getting-started/installing-sitecoredxg/advanced-installation/optional-install-the-default-rabbitmq-middleman-for-developers.md)
* [Upgrading and Downgrading](getting-started/upgrading-and-downgrading.md)
* [Downloads](getting-started/downloads.md)
* [Using SitecoreDXG](getting-started/using-sitecoredxg/README.md)
  * [Using the Default RabbitMQ Middleman and Trigger](getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger/README.md)
    * [Using the DocumentationConfiguration Object](getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger/using-the-documentationconfiguration-object.md)
  * [Using the Provided AWS S3 Deploy Completion Handler](getting-started/using-sitecoredxg/using-the-provided-aws-s3-deploy-completion-handler.md)
  * [Using the Provided Azure Blob Storage Deploy Completion Handler](getting-started/using-sitecoredxg/using-the-provided-azure-blob-storage-deploy-completion-handler.md)

## Architecture

* [Architecture Overview](architecture/architecture-overview.md)
* [Roles](architecture/roles/README.md)
  * [Role Combinations](architecture/roles/role-combinations.md)
* [Components](architecture/components-overview.md)
* [Plugins](architecture/plugins/README.md)
  * [Trigger Plugins](architecture/plugins/trigger-sub-component.md)
  * [Completion Handler Plugins](architecture/plugins/completion-handler-sub-component.md)
* [Middlemen](architecture/middlemen.md)
* [Understanding the Default RabbitMQ Middleman and Trigger](architecture/understanding-the-default-rabbitmq-middleman-and-trigger.md)

## How To

* [CI/CD Integration](how-to/cicd/README.md)
  * [Integrating the Default RabbitMQ Middleman](how-to/cicd/integrating-the-default-rabbitmq-middleman.md)
  * [Integrating the Default TeamCity RabbitMQ Meta-Runner](how-to/cicd/integrating-the-default-teamcity-rabbitmq-meta-runner.md)
* [Creating a Custom Trigger](how-to/creating-a-custom-trigger/README.md)
  * [Executing Documentation Generation](how-to/creating-a-custom-trigger/executing-documentation-generation.md)
  * [Executing Meta-Data JSON Generation](how-to/creating-a-custom-trigger/executing-meta-data-json-generation.md)
* [Slack and Microsoft Teams Integration](how-to/slack-and-ms-teams-integration/README.md)
  * [Integrating with Slack via Webhooks](how-to/slack-and-ms-teams-integration/integrating-with-slack-via-webhooks.md)
  * [Integrating with Microsoft Teams via Webhooks](how-to/slack-and-ms-teams-integration/integrating-with-ms-teams-via-webhooks.md)
* [Creating a Custom Completion Handler](how-to/creating-a-custom-completion-handler.md)
* [Creating a Custom Middleman](how-to/creating-a-custom-middleman.md)
* [Viewing Helix Validation Errors](how-to/viewing-helix-validation-errors.md)

## About the Generated Documentation

* [Overview](about-the-generated-documentation/overview.md)
* [Models](about-the-generated-documentation/models/README.md)
  * [Template Model](about-the-generated-documentation/models/template-model.md)
  * [Template Field Model](about-the-generated-documentation/models/template-field-model.md)
  * [Template Folder Model](about-the-generated-documentation/models/template-folder-model.md)
  * [Parent-Child Relationships of Models](about-the-generated-documentation/models/parent-child-relationships-in-models.md)
  * [Inheritance Relationship Model](about-the-generated-documentation/models/inheritance.md)
  * [Dependency Relationship Model](about-the-generated-documentation/models/dependencies.md)
* [Views](about-the-generated-documentation/views/README.md)
  * [Template View](about-the-generated-documentation/views/template-view.md)
  * [Template Field View](about-the-generated-documentation/views/template-field-view.md)
  * [Template Folder View](about-the-generated-documentation/views/template-folder-view.md)
  * [Parent-Child Relationship View](about-the-generated-documentation/views/parent-child-relationship-view.md)
  * [Inheritance Relationship View](about-the-generated-documentation/views/inheritance-relationship-view.md)
  * [Dependency View](about-the-generated-documentation/views/dependency-view.md)
* [Diagrams](about-the-generated-documentation/diagrams/README.md)
  * [SitecoreUML Syntax](about-the-generated-documentation/diagrams/sitecoreuml-syntax.md)
  * [Templates Diagram](about-the-generated-documentation/diagrams/templates-diagram.md)
  * [Template Folders Diagram](about-the-generated-documentation/diagrams/template-folders-diagram.md)
  * [Layer Diagrams](about-the-generated-documentation/diagrams/layer-diagrams.md)
  * [Module Diagrams](about-the-generated-documentation/diagrams/module-diagrams.md)
  * [Module Templates Diagrams](about-the-generated-documentation/diagrams/module-templates-diagrams.md)
* [Samples](about-the-generated-documentation/samples.md)

