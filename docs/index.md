---
menu: false
title: Welcome to cv4sensorhub
---

# Welcome to cv4sensorhub!

The cv4sensorhub (cv4s) framework is a .NET based C# environment to support the development of interdisciplinary applications utilizing state-of-the-art image processing technology. The highly flexible core data model allows for a wide variety of applications like marble thin section and sandstone image processing, white blood cell tracking, or even games.

## The framework

![CV4S Banner]({{ site.baseurl }}/assets/cv4s_banner.png){:.center-image}

The cv4sensorhub framework provides the following main services to support the domain specific application development:

  * Common data model based on polygons and raster images with arbitrary key-value pairs attached to them.
  * An increasing set of operations working on the data model including polygon operations, image segmentation, automatic annotations.
  * Support for a set of derived data (like neighbourhood graph of polygons) which is kept up-to-date automatically, whenever the data model changes.
  * Reusable user interface components for visualization
  * Persistance and communication functions to synchronize data with server side and other clients.
  * Statistics like "Maximal Grain Size" and neighbor number histograms, extended with Excel interoperability.
  * Machine learning and optimization methods to support the development of adaptive, smart operations.

![Framework architecture]({{ site.baseurl }}/assets/cv4sensorhub_architecture.png){:.center-image}

## Sample screenshot from the MinimalViewer

The screenshot below presents the uncustomized "MinimalViewer" application. Its goal is to expose all functionality of the framework. All domain specific applications utilize a subset of these capabilities and provide an ergonomic, domain specific user interface and design.

![Map screenshot of MinimalViewer]({{ site.baseurl }}/assets/terkep_demo_abra.png){:.center-image}
