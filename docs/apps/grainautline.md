---
parent: applications.md
menu: GrainAutLine
title: GrainAutLine
---

GrainAutLine is an application with state-of-the-art image processing functions designed for geology applications.
Its primary goal is to automate the analysis of thin section images as much as possible.

The current version aims for grain border detection, as this is a starting point for many applications. Once the grain boundaries are precisely known, several statistics like histogram of grain size or the number of neighboring grains can be easily retrieved.

![GrainAutLine logo]({{ site.baseurl }}/assets/grainUI.png "GrainAutLine UI"){:.center-image}

GrainAutLine follows a semi-automatic approach: a special drawing application is provided which has many high-level functions to accelerate the drawing of the grain boundaries. Our goal is to achieve an almost entirely automatic solution, but as this is not realistic in many applications, the user is given the chance to fully supervise all operations, and apply corrections whenever necessary. This way, the user does not have to rely on the automatic functions, but as the system is evolving, with time, less and less user interaction will be required.

The first application area of GrainAutLine is designed for the analysis of marble thin section images to retrieve the grain boundaries, even in the presence of twin crystal lines inside the grains.

![Original marble thin section and the grain boundaries]({{ site.baseurl }}/assets/MarvanyEsKonturEgyben.png){:.center-image}

We are also experimenting with an application area parallel to marble thin sections, which covers porosity and grain neighbour counting in sandstones.

![Sandstone neighborhood]({{ site.baseurl }}/assets/homokko_kicsi.png){:.center-image}

And the following screenshot shows the user interface of the previous, GrainAutLine 1 application. The user has just marked several areas to be merged into a single grain.

![The old GrainAutLine1]({{ site.baseurl }}/assets/GrainAutLine1_ui.png){:.center-image}

## Download and demos

Free download: the GrainAutLine application has a former, open source version which is freely available under the [GrainAutLine 1 homepage](http://bmeaut.github.io/grainautline/). The GrainAutLine2 application replacing the first one is also free of charge and will be published here as soon as the first version is released.

Demo video in hungarian: ![]({{ site.baseurl }}/assets/video.png){: .vertical-center-image } [Sandstone segmentation and neighbour counting (youtube)](https://youtu.be/jGhvGAUnBkA)

## Related publications
  * [Kristóf Csorba, Lilla Barancsuk, Balázs Székely and Judit Zöldföldi: "GrainAutLine - A Supervised Grain Boundary Extraction Tool Supported by Image Processing and Pattern Recognition", in Proceedings of Association for the Study of Marble &amp; Other Stones In Antiquity (ASMOSIA) XI. International Conference, Split, Croatia, 18-22. May 2015.](https://www.researchgate.net/publication/277597296_GrainAutLine_-_A_Supervised_Grain_Boundary_Extraction_Tool_Supported_by_ImageProcessing_and_Pattern_Recognition) (If you use GrainAutLine in any project, please cite this paper and drop us a line where GrainAutLine was cited, thank you!)
  * [Hajnal Máté (szakdolgozat): Síkidomok közel konvex felbontása márvány vékonycsiszolati képek feldolgozási céljából](http://diplomaterv.vik.bme.hu/hu/Theses/Sikidomok-kozel-konvex-felbontasa-marvany)
  * [Öllős Gábor (diplomaterv): Részben automatikus szemcsehatár meghatározás márvány vékonycsiszolati képeken, active contours alapokon](http://diplomaterv.vik.bme.hu/hu/Theses/Reszben-automatikus-szemcsehatar-meghatarozas)
  * [Szőts Ákos (diplomaterv): Márványvékonycsiszolat-elemző rendszer fejlesztése](http://diplomaterv.vik.bme.hu/hu/Theses/Marvanyvekonycsiszolatelemzo-rendszer)
  * [Barancsuk Lilla (szakdolgozat): Márványok osztályozása képfeldolgozás segítségével](http://diplomaterv.vik.bme.hu/hu/Theses/Marvanyok-osztalyozasa-kepfeldolgozas)
  * [Tamási Dénes (szakdolgozat): Grafikus márványmintázat szerkesztő és elemző alkalmazás fejlesztése](http://diplomaterv.vik.bme.hu/hu/Theses/Grafikus-marvanymintazat-szerkeszto-es-elemzo)
