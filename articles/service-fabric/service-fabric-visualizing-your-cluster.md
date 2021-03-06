﻿---
title: Visualizing your cluster using Azure Service Fabric Explorer | Microsoft Docs
description: Service Fabric Explorer is an application for inspecting and managing cloud applications and nodes in a Microsoft Azure Service Fabric cluster.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: ''

ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2018
ms.author: mikhegn

---
# Visualize your cluster with Service Fabric Explorer

Service Fabric Explorer (SFX) is an open-source tool for inspecting and managing Azure Service Fabric clusters. Service Fabric Explorer is a desktop application for Windows and Linux. Support for MacOS is coming soon.

## Service Fabric Explorer download

Use the following links to download Service Fabric Explorer as a desktop application:

- Windows
  - https://aka.ms/sfx-windows

- Linux
  - https://aka.ms/sfx-linux-x86
  - https://aka.ms/sfx-linux-x64

- macOS
  - https://aka.ms/sfx-macos

> [!NOTE]
> The desktop version of Service Fabric Explorer can have more or fewer features than the cluster support. You can fall back to the Service Fabric Explorer version deployed to the cluster to ensure full feature compatibility.
>
>

### Running Service Fabric Explorer from the cluster

Service Fabric Explorer is also hosted in a Service Fabric cluster's HTTP management endpoint. To launch SFX in a web browser, browse to the cluster's HTTP management endpoint from any browser - for example https://clusterFQDN:19080.

For developer workstation setup, you can launch Service Fabric Explorer on your local cluster by navigating to https://localhost:19080/Explorer. Look at this article to [prepare your development environment](service-fabric-get-started.md).

## Connect to a Service Fabric cluster
To connect to a Service Fabric cluster, you need the clusters management endpoint (FQDN/IP) and the HTTP management endpoint port (19080 by default). For example https://mysfcluster.westus.cloudapp.azure.com:19080. Use the "Connect to localhost" checkbox to connect to a local cluster on your workstation.

### Connect to a secure cluster
You can control client access to your Service Fabric cluster either with certificates or using Azure Active Directory (AAD).

If you attempt to connect to a secure cluster, then depending on the cluster's configuration you will be required to present a client certificate or log in using AAD.

## Video tutorial

To learn how to use Service Fabric Explorer, watch the following Microsoft Virtual Academy video:

> [!NOTE]
> This video shows Service Fabric Explorer hosted in a Service Fabric cluster, not the desktop version.
>
>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## Understand the Service Fabric Explorer layout
You can navigate through Service Fabric Explorer by using the tree on the left. At the root of the tree, the cluster dashboard provides an overview of your cluster, including a summary of application and node health.

![Service Fabric Explorer cluster dashboard][sfx-cluster-dashboard]

### View the cluster's layout
Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains. This placement ensures that your applications remain available in the presence of hardware failures and application upgrades. You can view how the current cluster is laid out by using the cluster map.

![Service Fabric Explorer cluster map][sfx-cluster-map]

### View applications and services
The cluster contains two subtrees: one for applications and another for nodes.

You can use the application view to navigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.

In the example below, the application **MyApp** consists of two services, **MyStatefulService** and **WebService**. Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas. By contrast, WebSvcService is stateless and contains a single instance.

![Service Fabric Explorer application view][sfx-application-tree]

At each level of the tree, the main pane shows pertinent information about the item. For example, you can see the health status and version for a particular service.

![Service Fabric Explorer essentials pane][sfx-service-essentials]

### View the cluster's nodes
The node view shows the physical layout of the cluster. For a given node, you can inspect which applications have code deployed on that node. More specifically, you can see which replicas are currently running there.

## Actions
Service Fabric Explorer offers a quick way to invoke actions on nodes, applications, and services within your cluster.

For example, to delete an application instance, choose the application from the tree on the left, and then choose **Actions** > **Delete Application**.

![Deleting an application in Service Fabric Explorer][sfx-delete-application]

> [!TIP]
> You can perform the same actions by clicking the ellipsis next to each element.
>
> Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, to enable automation.
>
>

You can also use Service Fabric Explorer to create application instances for a given application type and version. Choose the application type in the tree view, then click the **Create app instance** link next to the version you'd like in the right pane.

![Creating an application instance in Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> Service Fabric Explorer does not support parameters when creating application instances. Application instances use default parameter values.
>
>

## Next steps
* [Managing your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Service Fabric application deployment using PowerShell](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png