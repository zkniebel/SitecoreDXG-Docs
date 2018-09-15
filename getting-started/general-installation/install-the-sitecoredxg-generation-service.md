# Step 1: Install the SitecoreDXG Generation Service

The first step in installing SitecoreDXG is installing the Generation Service on the desired machine, keeping in mind that _**the SitecoreDXG Generation Service does not have to be installed on the same machine as the RabbitMQ server, the middleman or the Sitecore instance.**_

### Prerequisites

The installation instructions for the SitecoreDXG Generation Service assume that you have [node.js](https://nodejs.org/en/) and [npm](https://www.npmjs.com/) installed on the target machine prior to beginning the installation.

### Install the SitecoreDXG Generation Service

Once you have installed all of prerequisites installed, follow the instructions below to install the SitecoreDXG Generation Service on your machine:

1. Download the [`SitecoreDXG-Generation-Service-<version>.<build>.zip`](/getting-started/downloads.md) to your machine and extract in a location of your choosing. Note that it does not matter where you store it, and that the resulting directory will be your installation directory for the SitecoreDXG Generation Service.
2. \(Optional\) Open the `./settings.js` file and confirm or update the settings \(documented inline\) as needed
3. Install the SitecoreDXG Generation Service as a Windows Service by running the following command as an administrator in the installation directory: `npm run-script install-windows-service`.
   * Note that you can skip this step if you want to start the SitecoreDXG Generation Service manually from the command-line/PowerShell instead
   * Note that to uninstall the SitecoreDXG Generation Service, you can use the command `npm run-script uninstall-windows-service`
4. Go to the Services manager and ensure that the SitecoreDXG Generation Service is started
   * If it is started then feel free to customize startup and account settings for the service as desired
   * If it is not, check your SitecoreDXG logs \(stored in `C:/SitecoreDXG/Logs` by default, or in a custom location of your choosing if you have specified a different path in your `./Settings.js` file\) for errors or try starting the application manually from the command-line for troubleshooting
5. \(Optional\) Because SitecoreDXG doesn't automatically delete old output or log files, it is suggested that you set up a custom Windows scheduled task or something similar to perform the cleanup, in order to avoid your server running out of storage space. If you would like to set up a custom Windows scheduled task, [this article](https://jackworthen.com/2018/03/15/creating-a-scheduled-task-to-automatically-delete-files-older-than-x-in-windows/) can help to guide you through the process. Note that you can find the location of your logs and work directories by looking at your `./settings.js` file \(the default paths are `C:/SitecoreDXG/Work` and `C:/SitecoreDXG/Logs`\).

#### Important Note on When to Restart the SitecoreDXG Service

Anytime you change the `./settings.js` file you should restart your SitecoreDXG Generation Service. Some settings are okay to change without restarting the service, but most are not and the safest thing to do is restart the service. 



