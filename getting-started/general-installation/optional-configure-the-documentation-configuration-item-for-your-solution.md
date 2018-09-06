# Step 4: \(Optional\) Configure the Documentation Configuration Item for your Solution

_**Be sure that you have completed the installation of the **_[_**SitecoreUML Service for Sitecore**_](/getting-started/general-installation/install-the-sitecoreuml-service-for-sitecore.md)_** before proceeding with this step.**_

The latest version of the [SitecoreUML Service for Sitecore](https://github.com/zkniebel/SitecoreUML/releases/latest) includes a new _Documentation Configuration_ item, found at _/sitecore/system/Modules/SitecoreUML/Documentation Configuration_ \(by default; you can change this in the _SitecoreUML.config_\), that controls some of the options for how your documentation should be generated. Note that while setting up the _Documentation Configuration_ item is optional, **if you do not configure the item then none of the Helix Diagrams will be generated.**

Each of the following steps is optional, but recommended:

1. Provide a title for your documentation, by specifying it in the `Documentation Title` field.
2. For each layer, specify the root template folder item in the `[Foundation|Feature|Project] Layer Root` field.
3. For each layer, select the module folders that belong to the layer in the `[Foundation|Feature|Project] Module Folders` field.

As a side-note, it is worth mentioning that while the _Documentation Configuration_ item is included in the SitecoreUML Service for Sitecore, it is currently only used by SitecoreDXG. There are currently plans in place to rewrite the SitecoreUML Service for Sitecore to be a part of SitecoreDXG and to update SitecoreUML to call SitecoreDXG for reverse engineering and deployment needs.

