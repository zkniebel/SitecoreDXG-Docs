# Integrating SitecoreDXG into your CI/CD Pipeline

SitecoreDXG was designed for easy of integration with any CI/CD pipeline. If you are looking to integrate SitecoreDXG into your TeamCity-based pipeline, see [Integrating the Default TeamCity RabbitMQ Meta-Runner](integrating-the-default-teamcity-rabbitmq-meta-runner.md). Otherwise, if you are looking to integrate SitecoreDXG into Jenkins, Octopus Deploy, Travis, Codeship, GitLab, Buddy, Semaphore, or any other build tool then refer to the guide below.

### Integrating SitecoreDXG into your Build Pipeline via the Command Line

You can integrate SitecoreDXG into your CI/CD pipeline by completing the following two steps:

1. [Install the default RabbitMQ Middleman](../../getting-started/installing-sitecoredxg/general-installation/optional-install-the-default-rabbitmq-middleman.md) \(excluding the TeamCity Meta-Runner definition XML file\) on in a location that your build agent will have permissions to access
2. Add a new step to your build that executes the PowerShell script, below \(feel free to customize, rewrite or replace this script with your own written in the language of your choice\)

### Sample PowerShell Script to Call the Default RabbitMQ Middleman

```bash
## PARAMS #####################################

$scriptPath = "C:\path\to\rabbitmq-amqp-middleman.js"
$rabbitMQConnectionString = "http://localhost"
$serializerGetUrl = "http://uat-mysite.com/sitecoreuml/sitecoredxg/GetTemplateArchitecture"
$generationQueueName = "generation_queue__documentation"
$optionsJsonData = '{...}' # single-quotes intentionally used for proper parsing

## EXECUTION ##################################

Write-Output "Beginning execution..."

$scriptDir = (Get-Item $scriptPath).Directory.FullName
$currentLoc = Get-Location

Set-Location $scriptDir
npm install 
Set-Location $currentLoc

Write-Output "Dependencies installed"

$optionsFilePath = ".\$(New-Guid).json"
$optionsJsonData | Set-Content $optionsFilePath

Write-Output "Options JSON file generated at path $($optionsFilePath)"

Write-Output "Calling SitecoreDXG Middleman..."

node $scriptPath $rabbitMQConnectionString $serializerGetUrl $generationQueueName $optionsFilePath

Write-Output "Finished calling SitecoreDXG Middleman..."

Remove-Item $optionsFilePath

Write-Output "Cleaned up options JSON file"

Write-Output "Completed execution"
```

