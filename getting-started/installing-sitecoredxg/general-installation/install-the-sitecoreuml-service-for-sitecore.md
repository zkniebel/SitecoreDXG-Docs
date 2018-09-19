# 3. Install the SitecoreUML Service for Sitecore

The third step in the installation is to install the SitecoreUML Service for Sitecore, which is provided as a Sitecore package, on the Sitecore instance that you wish to generate the documentation for. As with the other components, _**the Sitecore instance can be installed on its own machine, the same machine as the SitecoreDXG components, or it can be otherwise hosted in the cloud**_.

To install the [SitecoreUML Service for Sitecore](https://github.com/zkniebel/SitecoreUML/releases/latest), follow the [installation and setup instructions](https://zkniebel.gitbooks.io/sitecoreuml/getting-started/setup-and-insta.html) in the SitecoreUML documentation.

Note that SitecoreDXG supports version 1.3.6+ of SitecoreUML.

## Important Security Note

The SitecoreUML Service for Sitecore is not meant to be a secure service and should only be installed on non-public, pre-production environments behind a firewall. In case you have the service installed on both your CM and public CD, note that the `SitecoreUML.CM.config` \(the config that registers the SitecoreUML service route\) must be deleted from the CD environment or else the endpoint would be open to the public. For more information, see the [SitecoreUML documentation](https://zkniebel.gitbooks.io/sitecoreuml/guide/sitecore-configuration.html#sitecoreumlcmconfig).

