

# Table of Contents

- [General Guidance](#general-guidance)
- [When to choose .NET Core for Docker Containers](#when-to-choose-net-core-for-docker-containers)
  * [Developing and deploying cross platform](#developing-and-deploying-cross-platform)
  * [Using containers for new projects](#using-containers-for-new-projects)
  * [Create and deploy microservices on containers](#create-and-deploy-microservices-on-containers)
  * [Deploying high density in scalable systems](#deploying-high-density-in-scalable-systems)
- [When to choose .NET Framework for Docker containers](#when-to-choose-net-framework-for-docker-containers)
  * [Migrating existing applications directly to a Windows Server container](#migrating-existing-applications-directly-to-a-windows-server-container)
  * [Using third-party .NET libraries or NuGet packages no available for .NET Core](#using-third-party-net-libraries-or-nuget-packages-no-available-for-net-core)
  * [Using .NET technologies, no available for .NET Core](#using-net-technologies--no-available-for-net-core)
  * [Using a platform or API that does not support .NET Core](#using-a-platform-or-api-that-does-not-support-net-core)
- [Decision table: .NET frameworks to use Docker](#decision-table--net-frameworks-to-use-docker)
- [What OS to target with .NET containers](#what-os-to-target-with-net-containers)
- [Official .NET Docker images](#official-net-docker-images)
  * [.NET Core and Docker image optimizations for development versus production](#net-core-and-docker-image-optimizations-for-development-versus-production)
    + [During development and build](#during-development-and-build)
    + [In Production](#in-production)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

# General Guidance

Use .NET Core with Linux or Windows Containers, for your containerized Docker server application when:

1. You have cross-platform needs. 

2. Your application architecture is based on microservices.

3. You need to start containers fast and want a small footprint per container to achieve better density or more containers per hardware unit in order to lower your costs.

Use .NET Framework for your containerized Docker server application when:

1. Your application currently uses .NET Framework and has strong dependencies on Windows.

2. You need to use Windows APIs that are not supported by .NET Core.

3. You need to use third-party .NET libraries or NuGet packages that are not available for .NET Core.

# When to choose .NET Core for Docker Containers

**Modularity and Lightweight nature**

When you deploy and start a container, its image is far smaller with .NET Core than with .NET Framework. In contrary, to use .NET Framework for a container, you must base your image on the Windows Server Core Image, which is a lot heavier than the Windows Nano Server or Linux images that you use for .NET Core.

Also, .NET Core is cross-platform, so you can deploy server apps with Linux or Windows container images. However, if you are using the traditional .NET Framework, you can only deploy images based on Windows Server Core.

## Developing and deploying cross platform

If your goal is to have an application that can run on multiple platforms supported by Docker, the right choice is .NET Core, because .NET Framework only supports Windows.

## Using containers for new projects

When you create and deploy a container, its image is far smaller with .Net Core than with .NET Framework.

## Create and deploy microservices on containers

## Deploying high density in scalable systems

# When to choose .NET Framework for Docker containers

## Migrating existing applications directly to a Windows Server container

## Using third-party .NET libraries or NuGet packages no available for .NET Core

## Using .NET technologies, no available for .NET Core

## Using a platform or API that does not support .NET Core

# Decision table: .NET frameworks to use Docker

# What OS to target with .NET containers

# Official .NET Docker images

## .NET Core and Docker image optimizations for development versus production

### During development and build

### In Production

 

 