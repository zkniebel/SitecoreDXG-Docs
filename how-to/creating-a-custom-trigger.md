# Creating a Custom Trigger

Writing a custom trigger for your SitecoreDXG server is meant to be as low-effort and straightforward a task as possible, to enable you to kick off your documentation generation in whatever way you see fit. To create a custom trigger, all you need to do is create a node module \(.JS file\) that looks similar to the below template:

```js
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

## Trigger Registration

The first thing that you should take note of in the above template is the `registerTrigger` function. This function is required, and has the job of performing the registration logic that binds the ID of the trigger to the function that should be called in order to start listening and executing the generation, which in this case is the `_registrationCallback` function.

Strictly speaking, the `TRIGGER_ID` property does not actually need to be made public via `exports`, but it is a good practice to do so anyway.

