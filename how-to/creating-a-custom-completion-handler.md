# Creating a Custom Completion Handler

While SitecoreDXG generates documentation for you, what do you do with the documentation once generation has completed is entirely up to you. SitecoreDXG supports the execution of one or more completion handlers after successful generation, and ships with an example completion handler, _helloWorld_, and a practical completion handler, [_AWS S3 Deploy_](/getting-started/using-sitecoredxg/using-the-provided-aws-s3-deploy-completion-handler.md), to help you create handlers of your own.

Completion Handlers can be self-contained modules, in that they can have their own _package.json_ files and their own local dependencies without having to modify the SitecoreDXG Generation Service's _package.json_ file in any way. If a _package.json_ file is detected for a completion handler, the completion handler module and its dependencies are automatically installed immediately before the SitecoreDXG Generation Service when calling `npm install` in the SitecoreDXG Generation Service's root.

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
 * @param {object} logger the logger
 * @param {Array<*>} params array of custom parameters
 */
var _execute = function (outputDirectoryPath, logger, params) {
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

The first thing that you should take note of in the above example is the `registerCompletionHandler` function. This function is required, and has the job of performing the registration logic that binds the ID of the completion handler to the function that should be called, which in this case is the `_execute` callback function, in order to run the desired logic on the generated output.

Strictly speaking, the `COMPLETIONHANDLER_ID` property does not actually need to be made public via `exports`, but it is a good practice to do so anyway.

## Adding a Custom Completion Handler to the SitecoreDXG Generation Service

In order to add a custom completion handler to the SitecoreDXG Generation Service, you need to perform the following steps:

1. Navigate to the `[SitecoreDXG-Installation-Root]/completion\_handlers` folder and copy in your custom completion handler file. SitecoreDXG will dynamically load all files in this folder as completion handlers. Note that it is recommended that you add your completion handler file into a sub-directory of the `./completion\_handlers` folder, e.g. `./completion\_handlers/Custom`, for better organization. 
2. \(Optional\) **If your custom completion handler uses third-party modules** then it is recommended that you create a _package.json_ file for it either manually or by calling `npm init` and then add the third-party modules to the package's dependencies. This will help keep your custom completion handler more self-contained and modular, while avoiding the need to make changes to the SitecoreDXG Generation Service's native _package.json_
3. \(Optional\) If you want your completion handler to run by default, then open the `[SitecoreDXG-Installation-Root]/settings.js` file and in the `configuration` object update the value of the `DefaultCompletionHandlers` property to the ID of your custom completion handler. This will tell SitecoreDXG that your custom completion handler should be registered and used after all successful generations unless a list of handlers to use is explicitly specified. 
4. **If your completion handler uses third-party modules and has its own **_**package.json**_** file **then be sure to run `npm install` in either the SitecoreDXG Generation Service root or in the completion handler's root to install the dependencies
5. **If you are running the SitecoreDXG Generation Service** as a Windows service then you need to restart the service

## Completion Handler Ideas

The following are some ideas for completion handlers that could be written for more robust generation setups:

* **Output Copy Handler: **copy the output from the output folder to a specific location on the SitecoreDXG Generation Service machine or a networked location
* **POST-Upload Output Handler:** uploads the output via POST request to a specified REST endpoint
* **Azure Blob Deploy Handler:** upload the output to Azure Blob Storage at a specific location from where it can be served to users \(directly or through a CDN\)
* **RabbitMQ Return Handler:** send the output back to the middleman or to another location by adding it to a result queue via RabbitMQ

**And more!** The point is that completion handlers are low-effort to implement and can serve any purpose that you need.

