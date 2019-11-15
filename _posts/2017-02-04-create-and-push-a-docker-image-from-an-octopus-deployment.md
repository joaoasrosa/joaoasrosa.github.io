---
layout: post
title: Create and Push a Docker Image from an Octopus Deployment
date: 2017-02-04 10:03:16.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Continuous Deployment
- Continuous Integration
- OSS
tags:
- ".NET"
- ".NET Core"
- Continuous Improvement
- Continuous Innovation
- Deployment
- DevOps
- Docker
- GitHub
- Octopus
- PowerShell
- VCS
meta:
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/MKqz2S6jUcZ
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _publicize_job_id: '1489352023'
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:15487188;s:56:"https://twitter.com/joaoasrosa/status/827819826349486081";}}
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=27794317&stype=M&topic=6233585522502041600&type=U&a=PADf
  _publicize_done_15638097: '1'
  _wpas_done_15487191: '1'
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2017/02/04/create-and-push-a-docker-image-from-an-octopus-deployment/"
---
[Docker](https://www.docker.com/) is one of the disruptive technologies within virtualization, allowing the different containers to run on the same machine, sharing resources, reducing the overhead. The technology allows DevOps teams to have another tool to develop, build and ship software. One use case for containers is the Microservices Architecture Pattern.

Background
----------

[DockerHub](https://hub.docker.com/) is the image repository offered by Docker, where we can publish public repositories (the tech community is there) or use the private repositories feature (instead of building an infrastructure in the local environment). One of the features is the [Automated Builds](https://docs.docker.com/docker-hub/builds/) from a GitHub or Bitbucket account. Although it is a great feature, not all software shops uses this set of technologies.

For a software shop using Octopus, there are already [features](https://octopus.com/docs/deploying-applications/docker-containers) to deploy Octopus images from an Octopus Deployment. However, is not possible to create and push a Docker Image based on packages stored in Octopus. To fill this gap, I create an Octopus step template where it is possible to create and push a Docker image to DockerHub.

This fits is an organisation moving from a VM environment to a Container environment, but keeping the current infrastructure, e. g., using Octopus to manage the releases (including where the packages are deployed).

The tools used for this tutorial were:

*   [Visual Studio 2015 Community Edition](https://www.visualstudio.com/)
*   [Docker for Windows](https://docs.docker.com/docker-for-windows/)
*   [Octopus Deploy Community Edition](https://octopus.com/)

Visual Studio and the Docker WebApp for the tutorial
----------------------------------------------------

Using the Visual Studio .NET Core Web Application template for this tutorial, the project was created and committed [here](https://github.com/joaoasrosa/DockerDotnetCoreDemo). The WebApp is the out-of-the-box web application.

Continuous Integration Server
-----------------------------

You can use your preferred CI server. In your CI server will need to:

1.  Publish the Docker WebApp.NET project
    
        dotnet publish WebAppDemo -c Release
    
2.  Create the NuGet package for Octopus
    
        Octo.exe pack --id DockerWebAppDemo --version 1.0.0
    
3.  Upload the AWS Lambda NuGet package to Octopus Server
    
        NuGet.exe push DockerWebAppDemo.1.0.0.nupkg -ApiKey myApiKey -Source https://myOctopusServer
    

These instructions are generic, and depending on your CI server technology can be done in different ways. You can take them as generic steps, and adapt to your needs.

Create and Push a Docker Image Octopus step template
----------------------------------------------------

The step template is simple and straightforward. The Powershell script:

1.  Get all the required parameters, such as the DockerHub username, password, image name, among others
2.  Validate the parameters, e. g., if they have a value
3.  Creates the Docker image
4.  Pushes the Docker image
5.  Feedback the user

The step template has a prerequisite; it depends on the Docker for Windows. You need to download and install it on the machines where the step will run.

Octopus Project
---------------

To create the Octopus image we need to use a pivot machine with Docker for Windows installed.

![octopus-docker](/images/assets/octopus-docker.png)

We will use the Octopus out-of-the-box features to deploy the DockerWebAppDemo package to the Pivot Machine, and the new step template to create and push the Docker image to DockerHub.

The Octopus Project will look like:

![docker-octopus-project](/images/assets/docker-octopus-project.png)

The first step deploys the NuGet DockerWebAppDemo package to a custom location in the Pivot Machine (with the Docker Machine role).

The second step creates and pushes the Docker image to DockerHub using the Dockerfile provided.

![docker-octopus-step](/images/assets/docker-octopus-step.png)

After creating a release (potentially triggered by the CI server), Octopus Server can deploy it.

![docker-octopus-deploy](/images/assets/docker-octopus-deploy.png)

If the step runs successfully we can check the Docker image in the repository.

![dockerhub-image](/images/assets/dockerhub-image.png)

Or even run it in a machine running Docker, using the following command:

    docker run -p 5000:80 -e "ASPNETCORE_URLS=http://+:80" -it --rm joaoasrosa/dockerwebappdemo

If we access to a browser using the URL:port for the Docker container, we can see the application running.

![docker-container-run](/images/assets/docker-container-run.png)

Final thoughts
--------------

The step allows the creation of Docker images from an Octopus deployment, centralising and minimising the packages maintenance operations. Also, it is possible to deploy the same package to a machine or a Docker image, increasing the deployment scenarios for a DevOps team.

The step template is under the [Octopus Library OSS](https://github.com/OctopusDeploy/Library). You can fork and add new features to it, or open an issue in [my fork](https://github.com/joaoasrosa/Library). All suggestions are welcome.
