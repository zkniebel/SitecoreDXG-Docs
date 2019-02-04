# Integrating with Microsoft Teams via Webhooks

As of version 1.1.0, SitecoreDXG now supports integration with Microsoft Teams for completion notifications via Incoming Webhooks. Like all logic that runs after generation completes, the Microsoft Teams integration is provided by a native [completion handler plugin](../../architecture/plugins/completion-handler-sub-component.md) that posts a message to the Microsoft Teams Incoming Webhook URL with some basic information about the generation and any [Helix validation errors](../../overview/helix-validation.md) that were identified. 

### Sample Notification

Depending on the information that you send in via the `DocumentationConfiguration` property of the [`OPTIONS_FILE_PATH`](../../getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger/) JSON object, you should see a notification similar to the following sample appear in your Teams channel after generation completes:

![SitecoreDXG Generation Completion Notification Sample](../../.gitbook/assets/teams-notification.png)

### Setup

Fortunately, Microsoft was nice enough to make setting up an Incoming Webhook for Teams super straightforward:

1. Follow the instructions to [set up a custom Incoming Webhook](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/connectors/connectors-using#setting-up-a-custom-incoming-webhook) 
2. Copy your new Incoming Webhook URL for use in the next step 
3. Create/update the [`OPTIONS_FILE_PATH`](../../getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger/) JSON object to be passed into your SitecoreDXG middleman to include the MS Teams completion handler and set its `Params.Url` property to your new Incoming Webhook URL, as follows:

```javascript
{
    DocumentationConfiguration: {},
    CompletionHandlers: [{
        ID: "MSTeams_Notifier",
        Params: {
            "Url": "https://outlook.office.com/webhook/XXXXXXXXXXXXXXXXXXXXXXXXX@XXXXXXXXXXXXXXXXXXXXXXXXXXXXX/IncomingWebhook/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
        }
    }]
}
```

Note that this completion handler supports the default supported [`DocumentationConfiguration`](../../getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger/using-the-documentationconfiguration-object.md) properties, and will display their information in the notification, including:

1. `DocumentationTitle`
2. `CommitAuthor`
3. `CommitHash`
4. `CommitLink`
5. `DeployLink`
6. `ProjectName`
7. `EnvironmentName`



