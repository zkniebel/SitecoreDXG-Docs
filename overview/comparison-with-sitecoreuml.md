# Comparison with SitecoreUML

SitecoreDXG comes from the SitecoreUML family and includes some of the same features and functionality, but the two are vastly different. 

* SitecoreDXG and SitecoreUML **do not share any of the same code**
* **SitecoreDXG was built specifically to be used without any GUI** tools, whereas SitecoreUML is heavily dependent on the GUI provided by the StarUML IDE
* **SitecoreDXG can be called directly from CI/CD pipelines**, meaning that it **can be run automatically without any manual intervention,** whereas SitecoreUML requires users to manually import architectures from Sitecore and then export the architecture to HTML documentation
* **SitecoreDXG does not require users to install and learn a new IDE/program** in order to use it, is **completely CLI-driven** and can be **called by a single command**; whereas SitecoreUML requires users to install and learn StarUML and the SitecoreUML tools within the StartUML IDE in order to use it
* **SitecoreDXG does not suffer from run-time rendering performance penalties during template import and diagram generation**, and is thus **significantly** faster \(similar to the benefits of using the VirtualDOM provided by React.js\)
* **SitecoreDXG proves helix validation tools** that validate template inheritance/dependencies against the Helix guidelines, whereas SitecoreUML does not
* **SitecoreDXG provides additional helix diagrams** that enable users to r**eview granular pieces of the architecture at the layer, module or module template level**, whereas SitecoreUML does not

### Further Details

It should be noted that while SitecoreUML supports the ability to create a new architecture from scratch and deploy it to Sitecore, SitecoreDXG does not currently support this functionality. Some of the other features of SitecoreUML that SitecoreDXG does not have direct support for include the ability to customize/update the documentation manually after import and a select few others. However, it is important to note that when SitecoreDXG generates documentation it also generates a MDJ project file that can be opened and edited in StarUML with the SitecoreUML tools. SitecoreUML is also capable of regenerating the documentation after these updates have been made. Additionally, SitecoreDXG can also be requested to just generate the MDJ project file and not to generate the documentation, which significantly reduces generation time in situations where customizations to the documentation are expected.

It is also worth noting that the fact that SitecoreUML and SitecoreDXG do not share any code is intended to change after SitecoreDXG's initial release. The plan is for SitecoreUML's import engine to be rewritten to directly call SitecoreDXG on import, and to use a "deferred rendering" strategy \(again, like the VirtualDOM provided by React.js\) to avoid the exponential performance penalty during import. This means that the remaining code and logic in SitecoreUML will effectively be a presentation and integration-layer wrapper that adds StarUML-based GUI support to SitecoreDXG.

Finally, the way that SitecoreDXG works is also very different from how SitecoreUML works. While the architecture of SitecoreUML will not be discussed in this documentation, the next section,_Architecture_, will cover in detail how SitecoreDXG functions.

