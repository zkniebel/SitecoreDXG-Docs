# Role Combinations

Some roles can also be combined to simplify the architecture in a variety of circumstances. By default, SitecoreDXG allows for the following role combination that can be created without customizing native code:

* **Middleman-Trigger: **implemented as a trigger component, this role is responsible for reaching out to the _serializer _directly and calling the _generator _with the retrieved data

In addition to the above, because - as will be discussed further in subsequent sections - the default component that satisfies the _serializer _role is the the SitecoreUML Service for Sitecore which is open-source, although it is not recommended that you customize or replace the SitecoreUML Service for Sitecore, doing so will enable you to make the following additional role combinations:

* **Serializer-Middleman: **implemented as a serializer component, this role is responsible for serializing the template architecture and passing it along to the _trigger_
* **Serializer-Middleman-Trigger: **implemented as a serializer component, this role is responsible for serializing the template architecture and directly calling the _generator _with the retrieved data



