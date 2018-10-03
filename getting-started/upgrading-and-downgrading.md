# Upgrading and Downgrading

Upgrading and downgrading SitecoreDXG is a pretty straightforward process. In order to upgrade or downgrade your installation of SitecoreDXG, perform the following steps:

1. \(If you **have not** installed SitecoreDXG as a Windows Service then skip to step 3\) Open a CMD/PowerShell window and navigate to your Generation Service's installation folder
2. Run the command `npm run-script uninstall-windows-service` to uninstall the Window Service for SitecoreDXG Generation Service
3. Backup/delete your SitecoreDXG installation folder
4. Follow the [Installation Instructions](installing-sitecoredxg/) to install the upgraded or downgraded version of SitecoreDXG



