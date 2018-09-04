# Creating a Custom Completion Handler

While SitecoreDXG generates documentation for you, what do you do with the documentation once generation has completed is entirely up to you. SitecoreDXG supports the execution of one or more completion handlers after successful generation, and ships with an example, _helloWorld_, completion handler to help you create handlers of your own.

It is expected that users will want to write their own and/or customize existing completion handlers for their specific use-cases, and it is assumed that completion handlers will be the most widely-customized piece of SitecoreDXG. For this reason, creating and customizing completion handlers is meant to be as low-effort and straightforward a task as possible, to enable you to use your generated output in whatever way you see fit.

To create a custom completion handler, you will need to create a node module \(.JS file\) that looks similar to the below example:

```js
#!/usr/local/env node

/*
 * Copyright (c) 2018 Zachary Kniebel. All rights reserved.
 *
 * NOTICE:  All information contained herein is, and remains the 
 * property of Zachary Kniebel. The intellectual and technical 
 * concepts contained herein are proprietary to Zachary Kniebel and
 * may be covered by U.S. and Foreign Patents, patents in process, 
 * and are protected by trade secret or copyright law. Dissemination 
 * of this information or reproduction of this material is strictly 
 * forbidden unless prior written permission is obtained from Zachary
 * Kniebel (contact@zacharykniebel.com).
 *
 */


/**
 * DEPENDENCIES
 */

// third-party
const winston = require("winston");

// local
const logger = require("../../logging.js").logger;


/**
 * CONSTANTS
 */

const COMPLETIONHANDLER_ID = "helloWorld!";


/**
 * FUNCTIONS
 */

/**
 * Executes the completion handler with the given output directory path 
 * @param {string} outputDirectoryPath the path to the output directory
 */
var _execute = function (outputDirectoryPath) {
  logger.info(`hello World! Output path is: "${outputDirectoryPath}"`);
};

/**
 * Registers the completion handler with the given CompletionHandlerManager - this function is required on all completion handler modules
 * @param {CompletionHandlerManager} completionHandlerManager the trigger manager to register the trigger for
 */
var registerCompletionHandler = function (completionHandlerManager) {
  completionHandlerManager.registerCompletionHandler(COMPLETIONHANDLER_ID, _execute);
};

exports.COMPLETIONHANDLER_ID = COMPLETIONHANDLER_ID;
exports.registerCompletionHandler = registerCompletionHandler;
```

The first thing that you should take note of in the above template is the `registerCompletionHandler` function. This function is required, and has the job of performing the registration logic that binds the ID of the completion handler to the function that should be called, which in this case is the `_execute` callback function, in order to run the desired logic on the generated output.

Strictly speaking, the `COMPLETIONHANDLER_ID` property does not actually need to be made public via `exports`, but it is a good practice to do so anyway.

