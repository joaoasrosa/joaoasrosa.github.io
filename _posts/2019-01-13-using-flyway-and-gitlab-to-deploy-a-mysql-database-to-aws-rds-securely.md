---
layout: post
title: Using Flyway and GitLab to deploy a MySQL database to AWS RDS securely
date: 2019-01-13 14:37:39.000000000 +01:00
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
- AWS
- CI/CD
- Flyway
- GitLab
- MySQL
- RDS
permalink: "/2019/01/13/using-flyway-and-gitlab-to-deploy-a-mysql-database-to-aws-rds-securely/"
comments: true
---
One of my passions is to be a trainer. Sharing knowledge, meeting new people, be continuously challenged, it fuels my brain, and I'm always learning something new. I'm creating a new training for software development teams, and one of the components is a MySQL database. Also, I'm using a public cloud provider (in this case AWS), and Xebia provides accounts to cover training, workshops and our own experiments.

All the application and infrastructure definition (code) is in GitLab. It gives a central place with source code and CI/CD. And I can automate everything! :) The stack is not up and running 24/7, and I do not like to repeat myself executing the scripts manually (in the end [I'm only human](https://www.youtube.com/watch?v=L3wKzyIN1yk), and I will fail in the script execution). Thus, I have a pipeline to validate and lint the CloudFormation templates, build the app and run the tests, deploy the CloudFormation template, deploy the database and finally deploy the app. Pretty standard nowadays.

To deploy the database, I decided to use [Flyway](https://flywaydb.org). It offers supports to different database technologies, and the Community version (free) has an interesting range of features, the features that I need to deploy the database. It also packs the Flyway CLI in a [Docker image](https://hub.docker.com/r/boxfuse/flyway/), which is precisely what I need for my GitLab pipeline.

Great! I can use the Docker image in my pipeline. My pipeline is multi-stage, and in each stage, I use different Docker images, with the tools needed for that particular stage. Separation of concerns, right?

My `.gitlab-ci.yml` looks like this (omitting parts of the script):

    stages:
      - validate
      - build
      - deploy
      - deploy-database
    
    validate:
      image: validate-image
      stage: validate
      ...
    
    build:
      image: build-image
      stage: build
      ...
    
    deploy:
      image: deploy-image
      stage: deploy
      ...
    
    deploy-database:
      image: boxfuse/flyway:5.2.4-alpine
      stage: deploy-database
      script:
        - export FLYWAY_PASSWORD=$DB_PASSWORD
        - flyway -configFiles=src/database/conf/flyway.conf info
        - flyway -configFiles=src/database/conf/flyway.conf migrate
        - flyway -configFiles=src/database/conf/flyway.conf info

If we take a close look at the `deploy-database` stage, it:

1.  Sets the database password from a secure environment variable
2.  Displays the information from the current database migration
3.  Execute the migrations
4.  Displays the information from the current database migration

Let's run it!

![](/images/assets/screenshot-2019-01-13-at-11.38.24.jpg)  

{:.image-caption}
*Using the Flyway image to deploy the database*

Errrggghhh... It fails. Taking a look into the [Dockerfile](https://github.com/flyway/flyway-docker/blob/bf62140795fcdcf8e16bc7038ac74eb88b66985c/alpine/Dockerfile#L14), I discovered why. The `entrypoint` is to the Flyway CLI tool, and it expects Flyway commands. Well, a way to bypass it is to create a new Docker image based on the Flyway image and set the `entrypoint` to `/usr/bin/env` for example. The Dockerfile:

    FROM boxfuse/flyway:5.2.4-alpine
    LABEL maintainers="João Rosa <https://joaorosa.io>"
    
    ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    
    ENTRYPOINT ["/usr/bin/env"]

Updating the stage `deploy-database` in `.gitlab-ci.yml` to use the new Docker image, and run it we have...

![](/images/assets/screenshot-2019-01-13-at-11.54.10.jpg)  

{:.image-caption}
*Successful run of the database deployment! Or not...*

The connection is **not secure**! That is not acceptable.  
Looking to the [MySQL documentation](https://dev.mysql.com/doc/refman/5.7/en/encrypted-connections.html), it is possible to explicitly indicate to use SSL in the connection. The Flyway URL will look like this: `jdbc:mysql://awesome.url:3306/myDatabase?autoReconnect=true&useSSL=true`. We can deploy it!

![](/images/assets/screenshot-2019-01-13-at-12.24.33.jpg)  

{:.image-caption}
*After enabling the SSL in the connection. Failed again...*

Hmmm... That is strange. Let's take a step back. If I'm using SSL, it needs to use a certificate. But the container is not aware of it. Time to use the Google skills, and looking for the documentation on how to connect to a MySQL RDS instance using SSL. AWS provides [it](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MySQL.html#MySQL.Concepts.SSLSupport). They have a certificate that can be used to authenticate with the service.

The Docker image needs to have the certificate, and given that the CLI is based on Java, we can add the certificate to the certificate store using the `keytool` CLI. The updated Dockerfile looks like:

    FROM boxfuse/flyway:5.2.4-alpine
    LABEL maintainers="João Rosa <https://joaorosa.io>"
    
    ARG STORE_PASS
    
    ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    
    ADD https://s3.amazonaws.com/rds-downloads/rds-combined-ca-bundle.pem ./
    
    RUN $JAVA_HOME/bin/keytool -keystore $JAVA_HOME/lib/security/cacerts -storepass $STORE_PASS -noprompt -trustcacerts -importcert -alias rds-combined-ca-bundle -file rds-combined-ca-bundle.pem
    
    ENV JAVA_ARGS=-Djava.security.egd=file:/dev/../dev/urandom -Djavax.net.ssl.trustStore=$JAVA_HOME/lib/security/cacerts -Djavax.net.ssl.trustStorePassword=$STORE_PASS
    
    ENTRYPOINT ["/usr/bin/env"]

As we can see, the certificate is downloaded, and using the `keytool` it is added to the certificate store. The environment variable `JAVA_ARGS` is updated to use the certificate store.

**NOTE:** as you can see it needs a password for the certificate store. For this post, I'm using an argument for the Dockerfile, using the secure environment variables from GitLab. However, **it is out of scope for this post** how to rotate and manage the secrets! You can use a parameter store from a public cloud provider, or software such as Hashicorp Vault. Out there are good articles on how to do it!

Using the new Docker image, we do another round:

![](/images/assets/screenshot-2019-01-13-at-12.41.49.jpg)

{:.image-caption}
*Database deployment using SSL*

As we can see, it deploys the database using an encrypted channel. Happy days, the pipeline is a bit more secure than before. :)
