# Slack and Microsoft Teams Integration

As of version 1.1.0, SitecoreDXG includes native support for Slack and Microsoft Teams integration for generation completion notifications. Slack and Microsoft Teams each have their own [completion handler plugin](../../architecture/plugins/completion-handler-sub-component.md) that may be leveraged at the user's discretion by passing an entry for the handler with the necessary parameters in the [`OPTIONS` argument in the call to the RabbitMQ middleman.](../../getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger.md) Both plugins work by leveraging the respective _Incoming Webhook_ functionality available in both Slack and Microsoft Teams.

{% page-ref page="integrating-with-slack-via-webhooks.md" %}

{% page-ref page="integrating-with-ms-teams-via-webhooks.md" %}

