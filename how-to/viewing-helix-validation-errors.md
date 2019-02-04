# Viewing Helix Validation Errors

As of SitecoreDXG 1.1.0, the new Helix Validation features have been implemented and validation errors can be reviewed in several ways.

### Diagrams

Invalid dependencies are automatically colored "red" in your diagrams. If a red dependency is displaying, view the dependency for more details. If you are looking at a [Layer Diagram](../about-the-generated-documentation/diagrams/layer-diagrams.md) or a [Module Diagram](../about-the-generated-documentation/diagrams/module-diagrams.md) and you are unsure of the source and target templates of the dependency then refer to the [Layer and Module Dependency Models](viewing-helix-validation-errors.md#layer-and-module-dependency-models) section below for more.

### Layer and Module Dependency Models

On the documentation page for the [Dependency Model](../about-the-generated-documentation/models/dependencies.md) that lives under the layer, e.g. `(Feature->Feature)`, or module, e.g. `(Multisite->Multisite)`, you can see all dependencies contained in the layer/module, including any invalid dependencies. Any entries with the `INVALID:...` prefix are invalid and will state the reason why the dependency is invalid, as well as the source and target template path information to help you track down the offending template\(s\).

### Dependency Models

On the model for the dependency itself you can see the same `INVALID:...` documentation for the dependency that you find on a [Layer or Module dependency model](viewing-helix-validation-errors.md#layer-and-module-dependency-models).

### Slack and Microsoft Teams Notifications

The completion handlers for Slack and Microsoft Teams natively display any validation errors detected during generation in the generation completion notifications that they send. For more information, refer to the [Slack integration](slack-and-ms-teams-integration/integrating-with-slack-via-webhooks.md) and [Microsoft Teams](slack-and-ms-teams-integration/integrating-with-ms-teams-via-webhooks.md) integration documentation pages.

### Custom

Remember that SitecoreDXG was designed specifically with extensibility in mind. All detected validation errors are passed to the completion handlers via the `metaball` parameter, thus you can create your own custom error handling logic that runs after generation has completed by [creating a custom completion handler](creating-a-custom-completion-handler.md).













