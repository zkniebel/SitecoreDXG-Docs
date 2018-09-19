# 4. \(Optional\) Configure the Documentation Configuration Item for your Solution

_**Be sure that you have completed the installation of the**_ [_**SitecoreUML Service for Sitecore**_](install-the-sitecoreuml-service-for-sitecore.md) _**before proceeding with this step.**_

The latest version of the [SitecoreUML Service for Sitecore](https://github.com/zkniebel/SitecoreUML/releases/latest) includes a new _Documentation Configuration_ item, found at _/sitecore/system/Modules/SitecoreUML/Documentation Configuration_ \(by default; you can change this in the _SitecoreUML.config_\), that controls some of the options for how your documentation should be generated. Note that while setting up the _Documentation Configuration_ item is optional, **if you do not configure the item then none of the Helix Diagrams will be generated**, but note that the item does not need to be published, unless your SitecoreUML Service for Sitecore is configured to retrieve data from the _web_ database.

## Configuring the _Documentation Configuration_ Item

Each of the following steps is optional, but recommended:

1. Provide a title for your documentation, by specifying it in the `Documentation Title` field.
2. For each layer, specify the root template folder item in the `[Foundation|Feature|Project] Layer Root` field.
3. For each layer, select the module folders that belong to the layer in the `[Foundation|Feature|Project] Module Folders` field.
   1. Note that module folders are not selected by the system, by default, so if do not select any module folders than no modules will appear in your layers and Helix Diagrams will not be generated for the modules
   2. Note that you may choose to select module group folders as module folders or you may select the individual modules within those module group folders. However, at this time identifying a module as belonging to a module group is not currently supported. 

### Why Do I have to Select the Module Folders?

SitecoreDXG needs to know the module folders in order to be able to generate the Helix Diagrams. Unfortunately, there is no reliable way to identify module folders, due to the fact that some modules live within module groups.

When the first version of the Helix Diagram features were initially created, they were developed for SitecoreUML and used Regular Expressions in order to determine which paths belonged to module folders. Despite being made user-configurable, this approach proved unreliable for varying architectures, and tedious for users to update. As such, the Regular Expression approach was abandoned for the implementation in SitecoreDXG and replaced with fields for selecting the modules that belong to each layer.

## Side-note

It is worth mentioning that while the _Documentation Configuration_ item is included in the SitecoreUML Service for Sitecore, it is currently only used by SitecoreDXG. There are currently plans in place to rewrite the SitecoreUML Service for Sitecore to be a part of SitecoreDXG and to update SitecoreUML to call SitecoreDXG for reverse engineering and deployment needs.

