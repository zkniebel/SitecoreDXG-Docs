# Step 1: Install the SitecoreDXG Generation Service

The first step in installing SitecoreDXG is installing the Generation Service on the desired machine, keeping in mind that _**the SitecoreDXG Generation Service does not have to be installed on the same machine as the RabbitMQ server, the middleman or the Sitecore instance.**_

### Prerequisites

The installation instructions for the SitecoreDXG Generation Service assume that you have [node.js](https://nodejs.org/en/) and [npm](https://www.npmjs.com/) installed on the target machine prior to beginning the installation.

### Step 1a: Install the [_node-canvas_](https://github.com/Automattic/node-canvas/wiki/Installation---Windows) dependencies

SitecoreDXG is dependent on [_node-canvas_](https://github.com/Automattic/node-canvas/wiki/Installation---Windows). To install SitecoreDXG, you must first have the dependencies for _node-canvas_ installed, which cannot be installed through a simple`npm install`. In the below, I have outlined the steps that you must take to install first the dependencies and then SitecoreDXG itself.

The easiest way to install the node-canvas dependencies is as follows:

1. Install node.js \(verified with 6.11.4+\)
2. Install chocolatey \(verified with 0.10.8+\)
3. Use chocolatey to install the rest of the dependencies
   * See below for important notes about installing the dependencies with Chocolatey
   * Be sure to adhere to the notes in the below and the installation instructions for [_node-canvas_](https://github.com/Automattic/node-canvas/wiki/Installation---Windows) exactly
   * If you run into installation issues, please see the "Common installation issues and solutions" section, below, and the installation instructions for [_node-canvas_](https://github.com/Automattic/node-canvas/wiki/Installation---Windows) before reaching out to me directly. If you are still unable to find the solution, reach out to me via Sitecore Community Slack \(@zachary\_kniebel\) and I will be happy to help.
4. Manually download GTK and unzip it to the path specified in the [_node-canvas_](https://github.com/Automattic/node-canvas/wiki/Installation---Windows) documentation

#### Important notes about the chocolatey installation

As part of the chocolatey dependency installation, it will try to install the Standalone VS2015 Build Tools: [Microsoft Build Tools 2015 Update 3](https://www.visualstudio.com/vs/older-downloads/) \(note that this is not the same as the "Microsoft Visual C++ 2015 Redistributable Update 3"\). However, if you have VS2015 already installed then this may not work. If that is the case, you will need to modify your installation and enable the C++ build tools. Note also that it MUST be VS2015 due to the expected folder path - VS2017 will not work, but you can have VS2017 installed side-by-side with VS2015 and/or the VS2015 build tools.

Once the build tools have been installed, you can easily install the rest with chocolatey, or you can install them manually. Instructions for installing the rest of the dependencies with chocolatey or manually can be found on the [Installation page of the \_node-canvas \_wiki](https://github.com/Automattic/node-canvas/wiki/Installation---Windows). When installing the rest of the dependencies, if you have any issues with the Visual C++ part \(CL.exe errors\) see [this issue](https://github.com/Automattic/node-canvas/issues/1015).

Lastly, don't forget about the Cairo installation. Even though Cairo is bundled with GTK, which will be installed by chocolatey, you still need to _manually_ download and unzip it to `C:\GTK`.

#### Common installation issues and solutions

If you installed your dependencies with chocolatey and/or used the standalone VS 2015 build tools installer then you may need to do one or both of the following:

* Run `npm config set msvs_version 2015 --global`before trying to install node-canvas to avoid "The tools version "2.0" is unrecognized. Available tools versions are..." errors
* Install the VS 2015 Build Tools from the 8.1 SDK \(do this only if you have issues with missing paths, as the SDK is very big\)

### Step 1b: Install the SitecoreDXG Generation Service

Once you have installed all of the [_node-canvas_](https://github.com/Automattic/node-canvas/wiki/Installation---Windows) dependencies in _Step 1a_, follow the instructions below to install the SitecoreDXG Generation Service on your machine:

1. Download the SitecoreDXG installation zip to your machine and extract in a location of your choosing. Note that it does not matter where you unzip and store the SitecoreDXG folder
2. Run`npm install`in the extracted installation folder.
   * If you see any Node-Canvas, Cairo, GTK, C++, MSBuild, or file path issues then refer back to the instructions for installing the dependencies in _Step 1a_
   * If the issue persists, attempt to run `npm install node-canvas --global`. If the command is successful, attempt to run `npm install`in the folder again. Otherwise, or if the `npm install`fails with a new error then refer back to the _Step 1a _\(dependency installation\).
   * If the issue continues, reach out to me over Sitecore Community Slack \(@zachary\_kniebel\) for further assistance.
3. \(Optional\) Open the _settings.js_ file and confirm or update the settings \(documented inline\) as needed
4. Install the SitecoreDXG Generation Service as a Windows Service by running the following command as an administrator in the installation folder: `npm run-script install-windows-service`.
   * Note that you can skip this step if you want to start the SitecoreDXG Generation Service manually from the command-line instead
   * Note that to uninstall the SitecoreDXG Generation Service, you can use the command `npm run-script uninstall-windows-service`
5. Go to the Services manager and ensure that the SitecoreDXG Generation Service is started
   * If it is started then feel free to customize startup and account settings for the service as desired
   * If it is not, check your SitecoreDXG logs for errors or try starting the application manually from the command-line for troubleshooting



