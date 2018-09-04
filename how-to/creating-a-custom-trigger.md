# Creating a Custom Trigger

Writing a custom trigger for your SitecoreDXG server is meant to be as low-effort and straightforward a task as possible, to enable you to kick off your documentation generation in whatever way you see fit. To create a custom trigger, all you need to do is create a node module \(.JS file\) that looks similar to the below:

```
#!/usr/local/env node

/**
 * DEPENDENCIES
 */

const generation = require("../../generation.js");

/**
 * CONSTANTS
 */

const TRIGGER_ID = "MyTrigger";

/**
 * FUNCTIONS
 */

var _registrationCallback = function () {
  ...your logic for listening and calling the generation function here...
};

/**
 * Registers the trigger for the given triggerManager - this function is required on all trigger modules
 * @param {object} triggerManager the trigger manager to register the trigger for
 */
var registerTrigger = function (triggerManager) {
  triggerManager.registerTrigger(TRIGGER_ID, _registrationCallback);
};

exports.TRIGGER_ID = TRIGGER_ID;
exports.registerTrigger = registerTrigger;
```

The first thing that you should take note of is the `registerTrigger` function. This function is required, and has the job of performing the registration logic that binds the ID of the trigger to the function that should be called in order to start listening and executing the generation, which in this case is the `_registrationCallback` function.

Strictly speaking, the `TRIGGER_ID` property does not actually need to be made public via `exports`, but it is a good practice to do so anyway.

## Executing Documentation Generation

In order to generate documentation, you need to call the `generateDocumentation` function of the `generation` module. 

The function has the following syntax:

```
generation.generateDocumentation(
  Object data,        // the parsed JSON data response received from the serializer
  Fn successCallback, // callback to be executed on successful generation
  Fn errorCallback,   // callback to be executed on generation error
);
```

Following this syntax, the below can be used to execute documentation generation:

```
generation.generateDocumentation(
  data,
  function (targetArchiveFilePath, targetArchiveFileName, targetFolderPath, targetHtmlDocFolderPath, targetMdjFilePath) {
    ...your logic to run on success...
  },
  function (error) {
    ...your logic to run on error...
  }
);
```

## Executing Meta-Data JSON Generation

SitecoreDXG uses the same third-party libraries as StarUML - the UML IDE that SitecoreUML integrates with - for documentation generation. As part of the documentation generation process, SitecoreDXG first generates a new Meta-Data JSON file \(.MDJ extension\), which is effectively a project file for StarUML. However, sometimes you may want just the MDJ file and not the HTML documentation, especially considering that the MDJ file may only take a few seconds to generate for a very complex solution, whereas the HTML documentation may take several minutes. For this reason, SitecoreDXG includes the abiltiy to execute the MDJ file generation independently of the HTML documentation generation.

In order to generate just the Meta-Data JSON file, you need to call the `generateMetaDataJson` function of the `generation` module. 

The function has the following syntax:

```
generation.generateMetaDataJson(
  Object data,        // the parsed JSON data response received from the serializer
  Fn successCallback, // callback to be executed on successful generation
  Fn errorCallback,   // callback to be executed on generation error
);
```

Following this syntax, the below can be used to execute the Meta-Data JSON file generation:

```
generation.generateMetaDataJson(
  data,
  function function (mdjPath, targetFileName, targetFolderPath, targetFilePath) {
    ...your logic to run on success...
  },
  function (error) {
    ...your logic to run on error...
  }
);
```





