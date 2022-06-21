---
toc: false
layout: post
description: Embedding the N5 Viewer in the Janelia Workstation
categories: [Data management,Java,N5,Visualization]
title: N5 Viewer plugin for Janelia Workstation
image: images/janeliaws-128.png
author: Konrad Rokicki
---

CellMap already has a great data portal for published data at [openorganelle.janelia.org](https://openorganelle.janelia.org/). But internally, before publishing, the data is spread across NFS file shares and sometimes difficult to find and access. Many of the tools used internally, such as BigDataViewer and Painter, are desktop applications which require direct access to the data through NFS/Samba mounting. Users need to be familiar with the disk organization and how to launch all of these tools.

The Janelia Workstation is a data discovery platform originally built for the FlyLight and MouseLight team projects. It makes data discoverable, easily accessible, and searchable, with group-based permissions to ensure everyone sees what they should be seeing. The Workstation platform was also recently [made available in the cloud](https://hortacloud.janelia.org/), but we were initially interested in using it internally at Janelia to enable access to pre-published data. The first step was done weeks ago, when Konrad added a *Synchronized Folders* feature to the Workstation, allowing any Workstation user to add a directory path to the Workstation, which is searched for N5 containers. These N5 containers are treated as first-class objects within the Workstation, and can be shared with other users, searched, added to virtual folders, etc.

For the hackathon, we wanted to embed the N5 Viewer into the Workstation, to make it possible to view and explore the N5 data sets in the Workstation.
To accomplish this, Konrad worked closely with N5 Viewer maintainer John Bogovic, BigDataViewer author Tobias Pietzsch, and N5/imglib2 creator Stephan Saalfeld. Drawing on their combined knowledge accelerated the effort tremedously.

## What was done

- N5 Viewer was first [refactored](https://github.com/saalfeldlab/n5-viewer/pull/24) such that the core viewer is now its own class and not a Fiji plugin. This allowed for the viewer to be embedded into programs other than Fiji.
- The refactored N5 Viewer was then [embedded](https://github.com/JaneliaSciComp/workstation/blob/d28d006c51c3fee40520a652098cb4c261dc1d6e/modules/ndviewer/src/main/java/org/janelia/workstation/ndviewer/BigDataViewerTopComponent.java#L112) into a Workstation *Top Component*, allowing it to be opened as part of the Workstation.
- We [implemented](https://github.com/JaneliaSciComp/workstation/blob/d28d006c51c3fee40520a652098cb4c261dc1d6e/modules/ndviewer/src/main/java/org/janelia/workstation/ndviewer/N5JadeReader.java) the `N5Reader` API using the Workstation's RESTful storage backend known as Jade. This gives us access to the data from the client without any NFS/Samba mounting.
- The n5-ij plugin's `N5DataDiscoverer` was used to [implement the data set nodes](https://github.com/JaneliaSciComp/workstation/blob/d28d006c51c3fee40520a652098cb4c261dc1d6e/modules/ndviewer/src/main/java/org/janelia/workstation/ndviewer/N5ContainerNode.java#L106) in the Workstation data explorer.
- Right-click actions [were added](https://github.com/JaneliaSciComp/workstation/blob/d28d006c51c3fee40520a652098cb4c261dc1d6e/modules/ndviewer/src/main/java/org/janelia/workstation/ndviewer/N5TreeNodeNode.java#L198) to the nodes, to allow users to open data sets in a new viewer or add them to an existing viewer.

Users can now browse the full list of CellMap images located in /groups/cellmap/cellmap (or add their own directories). Drilling into an N5 container reveals all of the data sets inside of it. Right-clicking on these data sets allows the user to open them instantly in N5 Viewer.

![]({{ site.baseurl }}/images/workstation_n5.png "The N5 Viewer running in the Janelia Workstation")

This proof of concept demonstrates the reusability of the N5 tools, the extensibility of the Workstation platform, and the power of having all your data accessible in one place, without copying.

## Possible future directions

- The sources in BigDataViewer should be named according to the n5 data sets
- We need to make the BigDataViewer menu options available somewhere
- The viewers should save/restore state like other components in the Workstation
- The first "killer app" might be saving the viewer state and then sharing it with other users as a predefined view of the data
- We can also link out to (or embed) other tools such as Paintera

