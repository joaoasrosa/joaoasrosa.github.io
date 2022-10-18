---
layout: post
title: 'Life of a C# Developer: How to build and test an AWS Lambda locally'
date: 2018-05-21 18:17:21.000000000 +02:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Cloud Computing
- Continuous Deployment
- OSS
tags:
- ".NET Core"
- Agile
- AWS
- AWS Lambda
- Continuous Improvement
- Linux
- Testing
- Windows
permalink: "/2018/05/21/life-of-a-c-developer-how-to-build-and-test-an-aws-lambda-locally/"
comments: true
excerpt: Today Serverless is a thing. Although everyone can write a blog post about how Serverless run on servers, I share the same visions as Mathias Verraes
---

Today Serverless is a thing. Although everyone can write a blog post about how Serverless run on servers, I share the same visions as [Mathias Verraes](https://twitter.com/mathiasverraes):

https://twitter.com/mathiasverraes/status/995317295072382976

Given that, I decided to share my developer experience building, testing and deploying AWS Lambda functions in the .NET world. Not a "Hello World" example, but rather a real-world scenario, where some services integrate with each other. Since a Serverless function is a tiny piece of code in a much larger process, **how can I test the flow on my development machine?**

Challenge
---------

In this example, we will have an AWS Lambda that receives a Notification from the Web Application and sends an SMS using a 3rd party provider. The requests and responses to the AWS Lambda function are proxied using AWS API Gateway, given all goodness of HTTP.

![AWS Lambda for SMS](/images/assets/aws-lambda-for-sms.png)

{:.image-caption}
*Representation of the interaction between the components*

However, the SMS provider does not have a sandbox which we can use for our acceptance tests, and we do not want to spend all of our credits. Since we want to be sure that our business code handles all the use cases, we need to build the behavior of the SMS provider ourselves. At least the documentation is up to a good standard. :)

![challenge-accepted-barney-stinson-06](/images/assets/challenge-accepted-barney-stinson-06.jpg)

{:.image-caption}
*Credits to [http://www.quickmeme.com](http://www.quickmeme.com)*

### Use Cases

We identified several uses cases which our business code (AWS Lambda) needs to handle:

1.  The account credentials are wrong. The authentication with the SMS provider will fail, and the SMS will not be sent
2.  The account doesn't have sufficient credits. To execute the operation, some credits will be used
3.  The SMS is sent. All good, SMS sent, credits deducted, happy days
4.  Rainy day. For some reason, the SMS provider doesn't return an expected result (described in the previous points). Thus we need to catch and handle it

### Testing Strategy

We want to have the feedback as quickly as we can, with different levels of testing. We have unit testing to make sure the business logic behaves based on the use cases. However, we also have acceptance tests in a Given/When/Then format, having a broader scope than the unit tests.

Implementation
--------------

Given the constraints described earlier, and to achieve the level of testing, we need to build a Testing API with the same behavior as the SMS provider.

### Testing API

The Testing API needs to be instrumented to behave according to the use case. The easiest route to do it is using an environment variable:

    switch (Environment.GetEnvironmentVariable("API_BEHAVIOUR"))
    {
      case "ok":
        return new OkResult();
      case "invalid_credentials":
        return new UnauthorizedResult();
      case "insufficient_credits":
        return new StatusCodeResult((int) HttpStatusCode.Forbidden);;
      default:
        return new StatusCodeResult((int) HttpStatusCode.InternalServerError);
    }

Using this approach we can control the response from the Testing API, allowing to assert the correct behavior of the Lambda function.

The Testing API is deployed in a Docker container, the same technology used by SAM Local. Reusing the same technology reduces the risk of friction in our development environment. However, it is possible to deploy the Testing API in other hosting technologies.

### SAM Local

AWS has built and released the Serverless Application Model (SAM) Local tooling. "**`sam`** is the AWS CLI tool for managing Serverless applications written with [AWS Serverless Application Model (SAM)](https://github.com/awslabs/serverless-application-model). SAM CLI can be used to test functions locally, start a local API Gateway from a SAM template, validate a SAM template, generate sample payloads for various event sources, and generate a SAM project in your favorite Lambda Runtime." \[1\]

The AWS Lambda function is triggered by an API Gateway event, sending the notification as SMS to the SMS provider.

The template has all the necessary components:

    AWSTemplateFormatVersion: 2010-09-09
    Transform: AWS::Serverless-2016-10-31
    Description: AWS SAM Local blog example
    
    Resources:
      Lambda:
        Type: AWS::Serverless::Function
        Properties:
          Handler: Lambda::Lambda.Function::Handler
          CodeUri: ./Lambda.zip
          Runtime: dotnetcore2.0
          Environment:
            Variables:
              SMS_API_URL: http://testing-api:80/
              SMS_API_USERNAME: foo
              SMS_API_PASSWORD: bar
          Events:
            PostEvent:
              Type: Api
              Properties:
                Path: /
                Method: post

As the template describes, the API Gateway will proxy a POST request to the AWS Lambda, which is responsible for executing the business code.

### Acceptance Tests

The Acceptance Tests aim to test the system behavior based on the specifications. The specifications were coded based on a set of Given/When/Then, where the tests are executed in a black box fashion (e. g. the system is tested without knowledge of the internals).

For every test run, a report is created. This is the default behavior of the testing framework ([LightBDD](https://github.com/LightBDD/LightBDD)). However, you can implement using your preferred poison. :)

The Acceptance Tests are responsible for starting the Testing API with the required behavior for the scenario under test; and also starts the SAM Local, calling the API Gateway command (`sam local start-api --docker-network testing`).

### Putting Everything Together

Since we are in the .NET world, we use [Cake](https://cakebuild.net) to script our local testing. The script allows the build, deploy and test the involved components in the [same way locally and in the CI server](http://joaorosa.io/2017/10/18/abstract-from-your-ci-use-cake/).

In this case, the script:

1.  Cleans the files from the previous build (binaries, artifacts, etc.)
2.  Restores the dependencies (NuGet)
3.  Builds the solution
4.  Run the Unit Tests
5.  Publish the AWS Lambda and the Testing API
6.  Package the AWS Lambda into a zip file
7.  Deploys the previously compressed AWS Lambda and the SAM template
8.  Creates the Docker container image for the Testing API
9.  Creates the Docker network for the components
10.  Run the Acceptance Tests
11.  Removes the Docker network
12.  Removes the Docker container image

The steps can be executed locally or on the CI server (see here for [TravisCI](https://travis-ci.org/joaoasrosa/aws-sam-local-blog). We have some limitations running in AppVeyor).

You can find the code here: [https://github.com/joaoasrosa/aws-sam-local-blog](https://github.com/joaoasrosa/aws-sam-local-blog)

Final thoughts
--------------

Serverless is a great technology, decreasing the necessary maintenance of the cloud components. However, like any technology, we should use it pragmatically. Since it's easy to put our code in a Function (or Lambda depending on the vendor), we can end with multiple asynchronous triggers in the cloud. Remember, back in the day, the use of triggers in the databases? Easy to develop, a pain to maintain. Same with Serverless code...

To decrease the risk of unintended behavior we need to have a sane CI/CD pipeline with a good level of testing. Also, we need to use the correct tools to allow faster feedback loops, starting in our development environment.

This post describes one possible way for .NET developers using AWS technologies. If you have a different but sane approach to achieve the same goal, just shout! ;)

#### References

\[1\] - [https://github.com/awslabs/aws-sam-cli](https://github.com/awslabs/aws-sam-cli)
