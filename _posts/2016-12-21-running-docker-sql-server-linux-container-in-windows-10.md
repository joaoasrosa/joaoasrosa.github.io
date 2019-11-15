---
layout: post
title: Running Docker SQL Server Linux container in Windows 10
date: 2016-12-21 14:43:55.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- SQL Server
tags:
- Docker
- Linux
- Windows 10
meta:
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _publicize_job_id: '30229744901'
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/SFUwgwFFQCL
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  _publicize_done_external: a:2:{s:7:"twitter";a:1:{i:15487188;s:56:"https://twitter.com/joaoasrosa/status/811582997531160580";}s:8:"facebook";a:1:{i:15487197;s:38:"https://facebook.com/10155076857243287";}}
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=27794317&stype=M&topic=6217348691129298944&type=U&a=QuYP
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
permalink: "/2016/12/21/running-docker-sql-server-linux-container-in-windows-10/"
---
Microsoft is doing a huge effort to bring SQL Server 2016 to Linux. Back in the summer, during the [Dublin 2016 SQL Saturday #501](http://www.sqlsaturday.com/501/eventhome.aspx), [Mark Souza](https://twitter.com/mark_azurecat) [presented the SQL Server history](https://onedrive.live.com/view.aspx?resid=56E37AA660DF4C78!370&ithint=file%2cpptx&app=PowerPoint&authkey=!AE6OLiox4aT1bNs). One of the major features is the ability to run SQL Sever 2016 on Linux.

Since then I added on my TODO list a simple task, test SQL Server in Linux. The best way to do it is using a Docker container, provided by Microsoft. Plus, since the last time that I played with Docker in Windows, they run on Hyper-V instead of VirtualBox. For me this is a huge increment in the product, thus we do not need several virtualization technologies on my development machine.

After installing the latest version of Docker (at the time of this post is 1.12.5), I start to read the [notes](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-setup-docker) on how to run the SQL Server Docker container. The first thing that jumped was this instruction:

    docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v HOSTDIRECTORY:/var/opt/mssql -d microsoft/mssql-server-linux

Especially the port assignment, since I've SQL Server installed on my development machine using the standard port 1433. I've modified the instruction to be:

    docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' -p 7000:1433 -v C:\Temp\Docker\mssql:/var/opt/mssql -d microsoft/mssql-server-linux

Where I assigned the public port 7000 to the container port 1433 (SQL Server default), and the container will persist the files in my file system at C:\\Temp\\Docker\\mssql.

Opening SQL Server Management Studio I can connect using my credentials:

![001](/images/assets/001.png)

After I connect just run the famous command:

    SELECT @@VERSION

and get the results:

![002](/images/assets/002.png)

I've played around for a few hours, and it is a good candidate to start the test for a production environment. I've tried a few applications and all of them worked without any problem. Good work SQL team, keep them going!
