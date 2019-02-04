# Integrating with Slack via Webhooks

As of version 1.1.0, SitecoreDXG now supports integration with Slack for completion notifications via Slack's Incoming Webhooks API. Like all logic that runs after generation completes, the Slack integration is provided by a native [completion handler plugin](../../architecture/plugins/completion-handler-sub-component.md) that calls the Slack API to post a message with some basic information about the generation and any [Helix validation errors](../../overview/helix-validation.md) that were identified. 

### Sample Notification

Depending on the information that you send in via the `DocumentationConfiguration` property of the [`OPTIONS_FILE_PATH`](../../getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger/) JSON object, you should see a notification similar to the following sample appear in your Slack channel after generation completes:

![SitecoreDXG Generation Completion Notification Sample](../../.gitbook/assets/slack-notification.png)

### Setup

Fortunately, Slack was nice enough to make the setup super straightforward:

1. [Create a new Slack App](https://api.slack.com/incoming-webhooks#getting-started) for your SitecoreDXG notifications \(you just enter a name and select your desired workspace\)
2. [Enable Incoming Webhooks](https://api.slack.com/incoming-webhooks#enable_webhooks) for your new app \(you just check the box to enable them for your app\)
3. [Create a new Incoming Webhook](https://api.slack.com/incoming-webhooks#create_a_webhook) for your new app \(you pick the channel that you want to post the messages to and click "Authorize"\)
4. Copy your new Incoming Webhook URL for use in the next step
5. Create/update the JSON file at your [`OPTIONS_FILE_PATH`](../../getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger/) with the options object to be passed into your SitecoreDXG middleman to include the Slack completion handler and set its `Params.Url` property to your new Incoming Webhook URL, as follows:

```javascript
{
    DocumentationConfiguration: {},
    CompletionHandlers: [{
        ID: "Slack_Notifier",
        Params: {
            "Url": "https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX"
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



