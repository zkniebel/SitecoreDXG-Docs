# Creating a Custom Trigger

Writing a custom trigger for your SitecoreDXG Generation Service is meant to be as low-effort and straightforward a task as possible, to enable you to kick off your documentation generation in whatever way you see fit. 

Triggers can be self-contained modules, in that they can have their own _package.json_ files and their own local dependencies without having to modify the SitecoreDXG Generation Service's _package.json_ file in any way. If a _package.json_ file is detected for a trigger, the trigger module and its dependencies are automatically installed immediately before the SitecoreDXG Generation Service when calling `npm install` in the SitecoreDXG Generation Service's root. 

To create a custom trigger, all you need to do is create a node module \(.JS file\) that looks similar to the below template:

```js
#!/usr/local/env node

/**
 * DEPENDENCIES
 */


/**
 * CONSTANTS
 */

const TRIGGER_ID = "MyTrigger";

/**
 * FUNCTIONS
 */

var _registrationCallback = function (configurationLoader, generation, logger) {
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

The first thing that you should take note of in the above template is the `registerTrigger` function. This function is required, and has the job of performing the registration logic that binds the ID of the trigger to the function that should be called in order to start listening and executing the generation, which in this case is the `_registrationCallback` function.

Strictly speaking, the `TRIGGER_ID` property does not actually need to be made public via `exports`, but it is a good practice to do so anyway.

## Adding a Custom Trigger to the SitecoreDXG Generation Service

In order to add a custom trigger to the SitecoreDXG Generation Service, you need to perform the following steps:

1. Navigate to the `[SitecoreDXG-Installation-Root]/triggers` folder and copy in your custom trigger file. SitecoreDXG will dynamically load all files in this folder as triggers. Note that it is recommended that you add your trigger file into a sub-directory of the `./triggers` folder, e.g. `./triggers/Custom`, for better organization. 
2. \(Optional\) **If your custom trigger uses third-party modules** then it is recommended that you create a _package.json_ file for it either manually or by calling `npm init` and then add the third-party modules to the package's dependencies. This will help keep your custom trigger more self-contained and modular, while avoiding the need to make changes to the SitecoreDXG Generation Service's native _package.json_
3. Open the `[SitecoreDXG-Installation-Root]/settings.js` file and in the `configuration` object update the value of the `Trigger` property to the ID of your custom trigger. This will tell SitecoreDXG that your custom trigger is the one that should be registered and used. 
4. **If your trigger uses third-party modules and has its own **_**package.json**_** file **then be sure to run `npm install` in either the SitecoreDXG Generation Service root or in the trigger's root to install the dependencies
5. **If you are running the SitecoreDXG Generation Service** as a Windows service then you need to restart the service



