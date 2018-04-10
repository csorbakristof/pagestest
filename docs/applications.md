---
menu: Applications
---

The applications built over the cv4sensorhub framework are presented in these subpages.

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
