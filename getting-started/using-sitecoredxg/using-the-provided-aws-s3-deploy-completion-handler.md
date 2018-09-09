# Using the Provided AWS S3 Deploy Completion Handler

SitecoreDXG includes the AWS S3 Deploy Completion Handler for deploying the generated output to an AWS S3 bucket. Using this completion handler, you can rapidly configure your CI/CD infrastructure to generate updated Sitecore template architecture documentation on every build, and then publish the generated HTML-based documentation to AWS for live viewing. This ensures that you always have an up-to-date and live documentation site for your architecture that you can optionally share with clients, internal teams, or other groups and individuals.

## Setup

1. Go to the [AWS Console](https://signin.aws.amazon.com) and create and/or retrieve the details for the AWS S3 bucket and user that you intend to use
   1. Create a new S3 bucket if you don't already have one that you intend to use
   2. In the AWS Console, create an IAM user with access to the bucket, if you don't already have one that you intend to use, and record the access key ID and secret access key for later use
   3. Configure the policy and management settings for your AWS S3 Bucket so that it can be served as a static website
   4. Configure the policy for your IAM user or its group \(group recommended\) so that the you can upload, download, list and delete objects to/from the S3 bucket
2. \(Optional\) if you wish to set the completion handler as the default then update the `DefaultCompletionHandlers` property in the `./settings.js` file with required settings for calling the completion handler
3. **If you are running the SitecoreDXG Generation Service** as a Windows service then you need to restart the service

## Parameters

The AWS S3 Deploy Completion Handler **requires a single parameter** that holds a JSON object with the following syntax:

```js
{
    "AccessKeyId": "YOUR_AWS_ACCESS_KEY_ID",
    "SecretAccessKey": "YOUR_AWS_SECRET_ACCESS_KEY",
    "S3BucketName": "MyS3Bucket",
    "S3FolderPath": "MySite/UAT"
}
```

In order to pass this object to the handler, it should be passed in as the first element of the `Params` array of the completion handler data. The following illustrates the completion handler data object for the AWS S3 Deploy Completion Handler within the completion handler data array:

```js
[{
    "ID": "AWS_S3",
    "Params": [{
        "AccessKeyId": "YOUR_AWS_ACCESS_KEY_ID",
        "SecretAccessKey": "YOUR_AWS_SECRET_ACCESS_KEY",
        "S3BucketName": "MyS3Bucket",
        "S3FolderPath": "MySite/UAT"
    }]
}]
```

### Important Note About Folders in AWS S3

The S3 buckets in AWS don't have a real concept of "folders", but S3 can be made to behave similar to the way you would expect it to if it did have folders, so long as you use a forward slash \(`/`\) as the delimiter of your path slugs. For example, in the above, the value `"MySite/UAT"` will effectively function as though the `/UAT` folder is a subdirectory of `/MySite`.

## Calling the S3 Deploy Handler Data from the Middleman

_This section describes how you can call the S3 Deploy Handler from the default RabbitMQ Middleman as well the provided TeamCity Meta-Runner._

1. Complete the steps described in the [Setup](#setup) section, above, on your SitecoreDXG Generation Server
2. Create your completion handler data object for the S3 Deploy Handler, as described above in the [Parameters](#parameters) section
3. Stringify your completion handler data array into the following syntax:
   ```js
   '[{\"ID\":\"AWS_S3\",\"Params\":[{\"AccessKeyId\":\"YOUR_AWS_ACCESS_KEY_ID\",\"SecretAccessKey\":\"YOUR_AWS_SECRET_ACCESS_KEY/mPoo+M5TjXgK1V\",\"S3BucketName\":\"MyS3Bucket\",\"S3FolderPath\":\"MySite/UAT\"}]}]'
   ```
4. Pass the strigified completion handler data array to the middleman so that it can be passed to the Trigger and subsequently to the Generator  
   1. **If using the default RabbitMQ middleman:** see [Using the Default RabbitMQ Middleman and Trigger](/getting-started/using-sitecoredxg/using-the-default-rabbitmq-middleman-and-trigger.md) for more information on the middleman parameters and syntax
   2. **If using the provided TeamCity Meta-Runner:** see [Integrating the Default TeamCity RabbitMQ Meta-Runner](/how-to/cicd/integrating-the-default-teamcity-rabbitmq-meta-runner.md) for more information on the fields and syntax


