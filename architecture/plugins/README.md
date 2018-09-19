# Plugins

SitecoreDXG was specifically designed to make it easy for developers to extend and customize it to suit their needs, and the most straightforward way to make modifications and customizations is through _plugins_. 

Plugins are independent node modules with their own dependencies that follow a specific structure in order to satisfy a particular [_role_](../roles/) of the SitecoreDXG ecosystem. There are two types of plugins supported by SitecoreDXG, natively: [_Trigger Plugins_](trigger-sub-component.md), and [_Completion Handler Plugins_](completion-handler-sub-component.md). 

Plugins are necessary because while SitecoreDXG was specifically built to be easily integrated into any CI/CD pipeline or automated process, there are always things that end-users might want to do differently or control based on their individual requirements. By enabling developers to write their own _trigger_ and _completion handler_ plugins, SitecoreDXG can be customized to suit nearly any need.

{% hint style="info" %}
By definition, plugins are technically [_components_](../components-overview.md), though they could be better described as _sub-components_ of the SitecoreDXG Generation Service.
{% endhint %}



