---
layout: post
title: Build a .NET Core 2.0 Application in AppVeyor
date: 2017-08-10 11:45:01.000000000 +02:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Continuous Integration
- OSS
tags:
- ".NET Core"
- AppVeyor
- Gist
- GitHub
- PowerShell
meta:
  _wpcom_is_markdown: '1'
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:15487188;s:56:"https://twitter.com/joaoasrosa/status/895581765506662400";}}
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _publicize_job_id: '8122770253'
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/g2HZDC5hkC4
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2017/08/10/build-a-net-core-2-0-application-in-appveyor/"
---
[AppVeyor](//www.appveyor.com/) is one of the Continuous Integration Services in the cloud, ready to use, with minimal configuration. It provides a Windows Server image with tooling to build, test and deploy ours .NET applications. Among the baseline software is .NET Core, however, the version is 1.0.4 (at the time of writing this post).

If we are playing around with .NET Core 2.0, AppVeyor doesn't offer the SDK (or the SDK build version that we need). Don't panic, it is possible to download and install other .NET Core SDKs into the instance during our build process. After poking the Internet, the .NET Team offers a [Powershell and a Bash script](//docs.microsoft.com/en-us/dotnet/core/tools/dotnet-install-script) to download and install the SDK by version.

Following the documentation, we can install any SDK version using the terminal/command line. The version that my project needs is `2.0.0-preview2-006497`. Let the games begin!

In a Powershell command line, I craft the command for my version, as:

    .\dotnet-install.ps1 -Version 2.0.0-preview2-006497

And Powershell informed me:

![Powershell dotnet_install.ps1 -Version 2.0.0-preview2-006497 command result](/images/assets/ps_dotnetinstall.png)

Hmmm, the required version doesn't exist in the blob. A roadblock... Nothing major. Opening the \[source code\][script\_source\_code](//github.com/dotnet/cli/blob/rel/1.0.0/scripts/obtain/dotnet-install.ps1) of the script, we can see that the [SDK download link is built](//github.com/dotnet/cli/blob/rel/1.0.0/scripts/obtain/dotnet-install.ps1#L396) based on a few parameters.

The .NET Team already did all the work regarding downloading, unpacking and installing the SDK, and I can leverage the script to get the SDK from another source. The official download link is [https://download.microsoft.com/download/F/A/A/FAAE9280-F410-458E-8819-279C5A68EDCF/dotnet-sdk-2.0.0-preview2-006497-win-x64.zip](//download.microsoft.com/download/F/A/A/FAAE9280-F410-458E-8819-279C5A68EDCF/dotnet-sdk-2.0.0-preview2-006497-win-x64.zip).

Doing a little tweak to [the file](//github.com/joaoasrosa/pullrequests-viewer/blob/master/build/install-dotnet.ps1#L396), it is possible to point the download of the SDK to the official download link:

    # $DownloadLinks = Get-Download-Links -AzureFeed $AzureFeed -AzureChannel $AzureChannel -SpecificVersion $SpecificVersion -CLIArchitecture $CLIArchitecture
    $DownloadLinks = @("https://download.microsoft.com/download/F/A/A/FAAE9280-F410-458E-8819-279C5A68EDCF/dotnet-sdk-2.0.0-preview2-006497-win-x64.zip")

At this point, I have all the individual components to make the final solution. The `appveyor.yml` file needs to execute the `dotnet_install` script before building the .NET Core 2 application:

    version: 0.0.{build}
    image: Visual Studio 2017 Preview
    build_script:
    - ps: >-
        ./build/install-dotnet.ps1
        dotnet --version
        # Build application
    test: off

And AppVeyor reports:

![AppVeyor installs the .NET Core 2.0 SDK](/images/assets/appveyor_build.png)

Hurray, I have .NET Core 2.0 SDK installed, and my application is built successfully! :)

You can use this solution to install _any_ version of the SDK that is not supported by the AppVeyor official image. You can jump to .NET Core 2.1!
