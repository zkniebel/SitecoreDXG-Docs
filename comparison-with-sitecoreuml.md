# Comparison with SitecoreUML

SitecoreDXG comes from the SitecoreUML family, leverages many of the same backing libraries and includes many of the same features and functionality, but the two do not share any of the same code. In contrast to SitecoreUML, SitecoreDXG was built specifically to be used without any GUI tools, whereas SitecoreUML is heavily dependent on the GUI provided by the StarUML IDE. Because of this, SitecoreDXG improves upon three of SitecoreUML's greatest areas of opportunity:

* SitecoreDXG can be called directly from CI/CD pipelines
* SitecoreDXG does not require users to install and learn a new IDE/program in order to use it
* SitecoreDXG does not suffer from run-time rendering performance penalties during template import and diagram generation, and is thus
  **significantly**
  faster \(similar to the benefits of using the VirtualDOM provided by React.js\)

It should be noted that while SitecoreUML supports the ability to create a new architecture from scratch and deploy it to Sitecore, SitecoreDXG does not currently support this functionality. Some of the other features of SitecoreUML that SitecoreDXG does not have direct support for include the ability to customize/update the documentation manually after import and a select few others. However, it is important to note that when SitecoreDXG generates documentation it also generates a MDJ project file that can be opened and edited in StarUML with the SitecoreUML tools. SitecoreUML is also capable of regenerating the documentation after these updates have been made. Additionally, SitecoreDXG can also be requested to just generate the MDJ project file and not to generate the documentation, which significantly reduces generation time in situations where customizations to the documentation are expected.

It is also worth noting that the fact that SitecoreUML and SitecoreDXG do not share any code is intended to change after SitecoreDXG's initial release. The plan is for SitecoreUML's import engine to be rewritten to directly call SitecoreDXG on import, and to use a "deferred rendering" strategy \(again, like the VirtualDOM provided by React.js\) to avoid the exponential performance penalty during import. This means that the remaining code and logic in SitecoreUML will effectively be a presentation and integration-layer wrapper that adds StarUML-based GUI support to SitecoreDXG.

Finally, the way that SitecoreDXG works is also very different from how SitecoreUML works. While the architecture of SitecoreUML will not be discussed in this documentation, the next section,_Architecture_, will cover in detail how SitecoreDXG functions.

