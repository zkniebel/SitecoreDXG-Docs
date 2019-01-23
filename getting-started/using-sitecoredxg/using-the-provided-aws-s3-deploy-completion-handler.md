# Using the Provided AWS S3 Deploy Completion Handler

SitecoreDXG includes the AWS S3 Deploy Completion Handler for deploying the generated output to an AWS S3 bucket. Using this completion handler, you can rapidly configure your CI/CD infrastructure to generate updated Sitecore template architecture documentation on every build, and then publish the generated HTML-based documentation to AWS for live viewing. This ensures that you always have an up-to-date and live documentation site for your architecture that you can optionally share with clients, internal teams, or other groups and individuals.

## Setup

1. Go to the [AWS Console](https://signin.aws.amazon.com) and create and/or retrieve the details for the AWS S3 bucket and user that you intend to use
   1. Create a new S3 bucket if you don't already have one that you intend to use
   2. In the AWS Console, create an IAM user with access to the bucket, if you don't already have one that you intend to use, and record the access key ID and secret access key for later use
   3. Configure the policy and management settings for your AWS S3 Bucket so that it can be served as a static website. The following is the JSON for a policy that could be used for a bucket named "mybucket":

      ```javascript
      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Sid": "PublicReadGetObject",
                  "Effect": "Allow",
                  "Principal": "*",
                  "Action": "s3:GetObject",
                  "Resource": "arn:aws:s3:::mybucket/*"
              }
          ]
      }
      ```

   4. Configure the policy for your IAM user or its group \(group recommended\) so that the you can upload, download, list and delete objects to/from the S3 bucket. The following is the JSON for a policy that could be used to give a user/group the necessary access to a bucket named "mybucket":

      ```javascript
      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Sid": "AllowUserReadWriteDeleteListDataObjectForMyBucketS3",
                  "Effect": "Allow",
                  "Action": [
                      "s3:PutObject",
                      "s3:ListBucket",
                      "s3:GetBucketLocation",
                      "s3:DeleteObject"
                  ],
                  "Resource": [
                      "arn:aws:s3:::*/*",
                      "arn:aws:s3:::mybucket"
                  ]
              }
          ]
      }
      ```
2. \(Optional\) if you wish to set the completion handler as the default then update the `DefaultCompletionHandlers` property in the `./settings.js` file of the SitecoreDXG Generation Service with required settings for calling the completion handler
3. **If you are running the SitecoreDXG Generation Service** as a Windows service then you need to restart the service

#### WARNING: You should always deploy to an empty directory

The AWS S3 Deploy Completion Handler is designed to perform clean deployments, meaning that any files in the targeted S3 folder will be deleted immediately prior to the deployment. You can use the `S3FolderPath` parameter to set the target deployment location to somewhere other than the bucket's root \(the default\). Note that anything in the target directory \(or the root if the target directory is not set\) will be deleted.

## Parameters

The AWS S3 Deploy Completion Handler requires a JSON object parameter with the following syntax:

```javascript
{
    "AccessKeyId": "YOUR_AWS_ACCESS_KEY_ID",
    "SecretAccessKey": "YOUR_AWS_SECRET_ACCESS_KEY",
    "S3BucketName": "MyS3Bucket",
    "S3FolderPath": "MySite/UAT"
}
```

In order to pass this object to the handler, it should be passed in as the `Params` object of the completion handler data. The following illustrates the completion handler data object for the AWS S3 Deploy Completion Handler within the completion handler data array:

```javascript
[{
    "ID": "AWS_S3",
    "Params": {
        "AccessKeyId": "YOUR_AWS_ACCESS_KEY_ID",
        "SecretAccessKey": "YOUR_AWS_SECRET_ACCESS_KEY",
        "S3BucketName": "MyS3Bucket",
        "S3FolderPath": "MySite/UAT"
    }
}]
```

### Important Note About Folders in AWS S3

The S3 buckets in AWS don't have a real concept of "folders", but S3 can be made to behave similar to the way you would expect it to if it did have folders, so long as you use a forward slash \(`/`\) as the delimiter of your path slugs. For example, in the above, the value `"MySite/UAT"` will effectively function as though the `/UAT` folder is a subdirectory of `/MySite`.

## Calling the S3 Deploy Handler Data from the Middleman

_This section describes how you can call the S3 Deploy Handler from the default RabbitMQ Middleman as well the provided TeamCity Meta-Runner._

1. Complete the steps described in the [Setup](using-the-provided-aws-s3-deploy-completion-handler.md#setup) section, above, on your SitecoreDXG Generation Server
2. Create your completion handler data object for the S3 Deploy Handler, as described above in the [Parameters](using-the-provided-aws-s3-deploy-completion-handler.md#parameters) section
3. Stringify your completion handler data into the options parameter, as follows:

   ```javascript
   '{\"CompletionHandlers\":[{\"ID\":\"AWS_S3\",\"Params\":{\"AccessKeyId\":\"YOUR_AWS_ACCESS_KEY_ID\",\"SecretAccessKey\":\"YOUR_AWS_SECRET_ACCESS_KEY",\"S3BucketName\":\"MyS3Bucket\",\"S3FolderPath\":\"MySite/UAT\"}}]}'
   ```

4. Pass the stringified object to the middleman so that it can be passed to the Trigger and subsequently to the Generator  
   1. **If using the default RabbitMQ middleman:** see [Using the Default RabbitMQ Middleman and Trigger](using-the-default-rabbitmq-middleman-and-trigger.md) for more information on the middleman parameters and syntax
   2. **If using the provided TeamCity Meta-Runner:** see [Integrating the Default TeamCity RabbitMQ Meta-Runner](../../how-to/cicd/integrating-the-default-teamcity-rabbitmq-meta-runner.md) for more information on the fields and syntax

