[//]: # (title: How to Configure CI/CD with JetBrains Space)
[//]: # (auxiliary-id: How to Configure CI/CD with JetBrains Space)

[JetBrains Space](https://www.jetbrains.com/space/) is a full-cycle collaboration solution for software development teams. This guide explains how to achieve continuous integration and delivery of JetBrains Space projects by integrating them with TeamCity.

Integration with TeamCity brings the following advantages to the JetBrains Space users:
* Compiling, testing, and deploying projects within the same environment.
* Building source code of pull requests, with the ability to merge sources automatically after a successful build.
* Extensive build overview: diffs and artifacts, detailed test reports on-the-fly, code coverage, inspections, and various other metrics.
* Flexible pipelines where builds depend on one another and share settings and results.
* Ability to configure builds as code, in Kotlin DSL.
* Cross-shared statuses of builds and code reviews, for easier monitoring.
* Authentication with a single account in both systems: VCS (Space) and CI/CD (TeamCity).

To perform all the described steps, you need to have:
* Administrative access to either the [TeamCity Cloud](https://www.jetbrains.com/teamcity/signup/) instance or [TeamCity On-Premises](https://www.jetbrains.com/teamcity/download/) server of your organization.
* Administrative access to the JetBrains Space instance of your organization.

If you only want to integrate JetBrains Space repositories with TeamCity projects, having project administration rights is enough.

## Building Sources of JetBrains Space Repository

There are three ways to integrate a JetBrains Space repository with TeamCity:
* Create a TeamCity project based on a repository.
* Create a build configuration based on a repository in an existing TeamCity project.
* Create a VCS root based on a repository in an existing TeamCity project.

We will describe the first approach as it the most popular and self-sufficient. However, you can always add one more Space [root](configuring-vcs-roots.md) or [build configuration](creating-and-editing-build-configurations.md#Creating+Build+Configuration+from+URL) to an existing project — tne procedure is similar.

This approach involves two steps: (1) creating a service application for TeamCity authentication in your Space instance, (2) creating a preset of connection to Space, and (3) creating a TeamCity project from a Space repository URL.

### Create Authentication Application in Space

In your JetBrains Space instance:
1. Go to __Administration | Applications__ and click __New application__.
2. Enter a convenient name (`Space-to-TeamCity` in our example), save the application, and click __Go to application settings__.
3. On the __Authorization__ tab, click __Configure requirements__. Enter the name of the Space project you are about to access from TeamCity.
4. Now, you need to set permissions that will be granted to the app in this project. Click __Configure__ and enable the following permissions:
    * General access / authentication:
        * _Members | View member profile_ (you might need a server administrator's approval for that)
    * Required for Commit Status Publisher:
        * _Git Repositories | Report external check status_ (if you are the project's administrator, you can approve this permission right in this __Authorization__ tab)
5. Go back to the app's __Overview__ and open the __Authentication__ tab.
6. Enable _Client Credentials Flow_.
7. To be able to use authentication via Space in TeamCity or/and to create projects/configurations from Space repositories, enable _Authorization Code Flow_ as well. Enter your TeamCity server's URL as the redirect URI.  
   To ensure that your TeamCity server can always connect to JetBrains Space, specify all the other possible endpoint addresses of the server. In most cases, it would be enough to specify the _Server URL_ set in __Global Settings__ in TeamCity. However, if you use a proxy for your TeamCity server but access this server directly, the authentication might not work unless the server's IP address is also specified here.
8. Copy the app's _Client ID_ and _Client secret_.

### Create Connection Preset

>TeamCity allows you to configure all settings of your _connection_ to VCS in one place and then reuse these settings in different projects and build configurations. If you add such a _connection_ on the <emphasis tooltip="root-project">Root project</emphasis> level, this will allow using its settings to connect any other project on the server. To make a connection available only in a certain project, you need to add it in this project.  
>You can configure as many connections as you want.

To create a connection to your JetBrains Space instance:

### Create Project

## Building Sources on JetBrains Space Pull Requests

## Reporting Build Statuses to JetBrains Space

## Displaying JetBrains Space Code Review Status in TeamCity

## Authenticating in TeamCity with JetBrains Space Account
