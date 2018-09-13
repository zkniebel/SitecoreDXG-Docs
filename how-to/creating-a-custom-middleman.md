# Creating a Custom Middleman

When it comes to creating a custom middleman, the sky is the limit as far as options for how to implement your middleman are concerned. Unlike custom triggers and completion handlers, there is very little structure that defines how your middleman must be implemented. More specifically, custom triggers and completion handlers must be written as node modules and must implement and export specific functions in order to work correctly, whereas a custom middleman can be written in any coding language that enables you to communicate with your _serializer_ and your _trigger_. Assuming that you are not replacing the SitecoreUML Service for Sitecore component \(which satisfies the _serializer_ role\), this means that so long as your language can communicate with the trigger and can make an HTTP GET to the SitecoreUML Service then your middleman should work.

If you decide to create a custom middleman, it is more than likely that you will want to create a custom trigger, as well. For example, you may want to make a middleman that performs all communication with SitecoreDXG through web requests. In this case, you may choose to create a new trigger that exposes an ExpressJS service \(or you could build off of the example ExpressJs that is included with SitecoreDXG\), and write your custom middleman as a PowerShell script, or as part of an application written in C\#, Java, Bash, C++, PHP, C, Lisp, ... and so on. 

## Requirements of a Middleman

At a minimum, a middleman must be able to satisfy the following responsibilities:

* Retrieving the serialized Sitecore template architecture from the _serializer_ \(the SitecoreUML Service for Sitecore, by default\)
* Forwarding the response from the _serializer_ to the _trigger_

In addition to the above, the native RabbitMQ middleman also includes support for adding _completion handler_ data to the serialized response before passing it along to the trigger. Doing so will enable you to specify the completion handler\(s\) and settings to be used for each specific execution. If your middleman is being used to integrate with a CI/CD tool, for example, this means that you can have unique setting per build/environment, and beyond. As such, it's best practice for middlemen to also include support for adding completion handler data to the serialized response.

## Example

The below example shows the default RabbitMQ Middleman that is included with SitecoreDXG. Feel free to use this as a starting point when writing your own handlers.

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
 
/* DEPENDENCIES */

// third-party
const amqp = require('amqplib/callback_api');
const request = require('request');

/* EXECUTION */

/**
 * Optionally closes the connection and exits with the given exit code
 * @param {object} process process object to exit
 * @param {integer} exitCode exit code value to be passed upon exiting  
 * @param {object} connection (optional) connection to be closed
 */
var _exitProgram = function(process, exitCode, connection) {
    if (connection) {
        connection.close(); 
    }

    process.exit(0);
};


var args = process.argv.slice(2);
var connectionString = args[0];

if (!connectionString) {
    console.log("No connectionString was passed. Program terminating without sending.");
    return;
}

amqp.connect(connectionString, function(err, conn) {
    // create a channel
    conn.createChannel(function(err, ch) {
        var jsonGetUrl = args[1];        
        if (!jsonGetUrl) {
            console.log("No jsonGetUrl was passed. Program terminating without sending.");
            _exitProgram(process, 1, conn);
            return;
        }

        var queue = args[2];     
        if (!queue) {
            console.log("No queue was passed. Program terminating without sending.");
            _exitProgram(process, 1, conn);
            return;
        }

        request(jsonGetUrl, (err, res, data) => {
            if (err) { 
                return console.error(err); 
                _exitProgram(process, 1, conn);
            }
            
            var json = JSON.parse(data);
            if (!json.Success) {
                console.error("An error occurred while retrieving the architecture data. Program terminating...", json);
                _exitProgram(process, 1, conn);
            }            
            if (args.length > 3) {
                var completionHandlers = args[3];
                json.Data.CompletionHandlers = JSON.parse(completionHandlers);
                data = JSON.stringify(json);
            }

            console.log("Architecture data received. Forwarding to generation_queue...");
            ch.assertQueue(queue, {durable: false});
            ch.sendToQueue(queue, Buffer.from(data));
            console.log(" [x] Sent %s bytes to the generation_queue", data.length);

            setTimeout(function() { _exitProgram(process, 0, conn) }, 500);
        });
    });
});


```







