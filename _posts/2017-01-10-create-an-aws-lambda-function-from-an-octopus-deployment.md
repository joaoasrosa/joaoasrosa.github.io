---
layout: post
title: Create an AWS Lambda function from an Octopus Deployment
date: 2017-01-10 12:27:40.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Cloud Computing
- Continuous Deployment
- Continuous Integration
- OSS
tags:
- ".NET"
- ".NET Core"
- AWS
- AWS Lambda
- Deployment
- DevOps
- GitHub
- NuGet
- Octopus
- PowerShell
- Visual Studio
meta:
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/KTpJMW2yTdY
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _publicize_job_id: '602035564'
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  _publicize_done_external: a:2:{s:7:"twitter";a:1:{i:15487188;s:56:"https://twitter.com/joaoasrosa/status/818796469658517505";}s:8:"facebook";a:1:{i:15487197;s:38:"https://facebook.com/10155143202503287";}}
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=27794317&stype=M&topic=6224562163344777216&type=U&a=liFo
  _publicize_done_15638097: '1'
  _wpas_done_15487191: '1'
  _publicize_done_15638104: '1'
  _wpas_done_15487197: '1'
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2017/01/10/create-an-aws-lambda-function-from-an-octopus-deployment/"
---
[AWS Lambda](https://aws.amazon.com/lambda/) is one of the AWS Compute Services, alongside with [Amazon EC2](https://aws.amazon.com/ec2/) or [Amazon EC2 Container Service](https://aws.amazon.com/ecs/). In a nutshell, AWS Lambda is the serverless offer from AWS, allowing "you run code without provisioning or managing servers"\[1\].

In the DevOps spirit, and using [Octopus](https://octopus.com/) as the Continuous Deployment tool, I couldn't find a step template to create an AWS Lambda function. If it doesn't exist, create it and give it away!

Background
----------

AWS Lambda supports a broad range of technologies, such as Java, Python or NodeJS. The new kid on the block was .NET Core, [announced](https://aws.amazon.com/blogs/compute/announcing-c-sharp-support-for-aws-lambda/) on 1st of December 2016. It was a good announcement for Microsoft tech shops, having another tool in the toolbelt.

The tools used for this demo were:

*   [Visual Studio 2015 Community Edition](https://www.visualstudio.com/)
*   [AWS Toolkit for Visual Studio](https://aws.amazon.com/visualstudio/)
*   [AWS Tools for Windows Powershell](https://aws.amazon.com/powershell/)
*   [Octopus Deploy Community Edition](https://octopus.com/)

Visual Studio and AWS Lambda Function Project
---------------------------------------------

Using one of the Visual Studio AWS Lambda templates for the demo, the project was created and committed [here](https://github.com/joaoasrosa/AWSLambdaDemo). In a nutshell, the AWS Lambda function receives an Amazon S3 event and returns the S3 object Content Type. Simple and straightforward.

Continuous Integration Server
-----------------------------

You can use your preferred CI server. In your CI server will need to:

1.  Publish the AWS Lambda .NET project
    
        dotnet publish AWSLambdaDemo -c Release
    
2.  Zip the published AWS Lambda .NET project
3.  Create the NuGet package for Octopus
    
        Octo.exe pack --id AWSLambdaDemo --version 1.0.0.0
    
4.  Upload the AWS Lambda NuGet package to Octopus Server
    
        NuGet.exe push AWSLambdaDemo.1.0.0.0.nupkg -ApiKey myApiKey -Source https://myOctopusServer
    

These instructions are generic, and depending on your CI server technology can be done in different ways. You can take them as generic steps, and adapt to your needs.

 Create AWS Lambda function Octopus step template
-------------------------------------------------

The step template is simple and straightforward. The Powershell script:

1.  Checks if the AWS Tools for Windows Powershell is installed
2.  Get all the required parameters, such as the access keys, region, function name, among others
3.  Validate the parameters, e. g., if they have a value
4.  Execute the operation
5.  Feedback the user

The step template has a prerequisite, it depends on the AWS Tools for Windows Powershell. You need to download and install it on the machines where the step will run.

Octopus Project
---------------

To create the AWS Lambda function, we need to use a pivot machine. At the moment is not possible to publish it directly to AWS.

![octopus2awslambda](/images/assets/octopus2awslambda.png)

We will use the Octopus out-of-the-box features to deploy the AWSLambdaDemo package to the Pivot Machine, and the new step template to publish the function to AWS.

The Demo Octopus Project will look like this:

![octopus-project](/images/assets/octopus-project.png)

The first step just deploys the upload NuGet AWSLambdaDemo package to a custom location in the Pivot Machine (with the role AWS Lambda Demo).

The second step creates the AWS Lambda from the deployed NuGet AWSLambdaDemo package from the custom location.

![octopus-aws-step](/images/assets/octopus-aws-step.png)

After creating a release (potentially triggered by the CI server), Octopus Server can deploy it.

![octopus-aws-deploy](/images/assets/octopus-aws-deploy.png)

And voilá! A new AWS Lambda function is deployed!

![aws-lambda](/images/assets/aws-lambda.png)

Final thoughts
--------------

The step template is under the [Octopus Library OSS](https://github.com/OctopusDeploy/Library). You can fork and add new features to it, or open an issue in [my fork](https://github.com/joaoasrosa/Library). All suggestions are welcome.

\[1\] - [http://docs.aws.amazon.com/lambda/latest/dg/welcome.html](http://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
