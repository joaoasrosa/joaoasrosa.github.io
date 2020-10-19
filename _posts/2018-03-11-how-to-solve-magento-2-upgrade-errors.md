---
layout: post
title: How to solve Magento 2 upgrade errors
date: 2018-03-11 12:54:21.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Continuous Deployment
- Continuous Integration
- Magento 2
- OSS
tags:
- Linux
- Magento2
permalink: "/2018/03/11/how-to-solve-magento-2-upgrade-errors/"
comments: true
---
Magento 2 is the leading Open Source Software for e-commerce, with a vibrant community and proper product documentation.

The development team releases bug fixes and new features in a regular cadence, given support to security threats, market trends, amongst others.

Environment
-----------

The environment is [deployed in AWS](https://anotherlookontech.wordpress.com/2018/01/14/migrate-magento-from-on-premises-to-the-cloud/), using an immutable infrastructure. It allows us to deploy several development/testing environments where we can develop the scripts to automate the upgrade process for our CI/CD pipeline. Also, it is our workbench for testing UI changes, new plugins, amongst others.

Upgrading
---------

However, trying to upgrade to the latest version (at the moment of writing this post is 2.2.3), using the [official documentation](http://devdocs.magento.com/guides/v2.2/comp-mgr/cli/cli-upgrade.html), we receive the following error:

![magento2_upgrade_004](/images/assets/magento2_upgrade_004.png)

{:.image-caption}
*Magento 2 upgrade command - failed to open stream error*

This is annoying. So far, we had reliable platform upgrades. Using my developer hat, we followed the error. A file was missing in the `magento 2 installation path\setup\` folder.

Doing a quick search with the `ls` command, we had the folder structure:

![magento2_upgrade_003](/images/assets/magento2_upgrade_003.png)

{:.image-caption}
*Magento 2 root folder - after the ls command*

The code never lies. The `setup`/ folder doesn't exist. It intrigued us, getting us to investigate why the folder wasn't there. We verified:

*   The [official GitHub repo](https://github.com/magento/magento2/tree/2.2). The `setup/` folder exists, and it has content
*   Download the official [Magento 2 Full Release](https://magento.com/tech-resources/download), inspecting the contents. Again, the `setup/` folder exists, and it has content
*   Deploy a new AWS development environment with the current infrastructure, inspecting the folder structure. The `setup/` folder **exists** in the current installation

![magento2_upgrade_001](/images/assets/magento2_upgrade_001.png)

{:.image-caption}
*Magento 2 root folder - current installation*

Given the information from our investigation, it seemed to point out to the PHP Composer, which doesn't deploy the `setup/` folder during the upgrade process. To prove it, we tried to upgrade the environment again, using the same commands:

![magento2_upgrade_002](/images/assets/magento2_upgrade_002.png)

{:.image-caption}
*Magento 2 composer - update command*

And we were able to reproduce the initial error. At least it is reproducible and supports our theory. :)

The (temporary) solution
------------------------

Since the PHP Composer package should contain (apart from the metadata file) the same files as  the downloadable Magento 2 installation package, we've tried to:

*   Follow the upgrade steps from the official guide **until step 6** (_Update the database schema and data_)
*   Download the Magento 2 installation package
*   Extract the `setup/` folder to the Magento 2 installation folder
*   Resume the Magento 2 upgrade process

And voilá, it finished the Magento 2 upgrade to the version 2.2.3. Happy days, we can do our testing on the new version of the shop, before promoting it to production.

This error had been reported to the Magento development team, however, they can't reproduce it. Nevertheless, we can use this workaround to upgrade our (your) shop.
