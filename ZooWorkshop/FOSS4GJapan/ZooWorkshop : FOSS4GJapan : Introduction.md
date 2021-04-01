## Introduction

\_\_TOC\_\_ [table of content](ZooWorkshop : FOSS4GJapanWorkShop "wikilink") \|
[//ZooWorkshop/FOSS4GJapan/UsingZooFromOSGeoLiveVMNext](ZooWorkshop : FOSS4GJapan : UsingZooFromOSGeoLiveVMNext "wikilink")

### What is ZOO ? {#what_is_zoo}

ZOO is a WPS (Web Processing Service) open source project recently
released under a [MIT/X-11](Licence "wikilink")
style license. It provides an OGC WPS compliant developer-friendly
framework to create and chain WPS Web services. ZOO is made of three
parts:

-   [   ZOO Kernel](ZooWebSite : ZooKernel : Introduction "wikilink"): A powerful server-side C Kernel which makes it
    possible to manage and chain Web services coded in different
    programming languages.
-   [   ZOO Services](ZooWebSite : ZooServices : Introduction "wikilink"): A growing suite of example Web Services based on
    various open source libraries.
-   [ZOO    API](ZooWebSite : ZOOAPI : Introduction "wikilink"): A server-side JavaScript API able to call and chain the ZOO
    Services, which makes the development and chaining processes easier.

ZOO is designed to make the service development easier by providing a
powerful system able to understand and execute WPS compliant queries. It
supports several programming languages, thus allowing you to create Web
Services in your favorite one and from an already existing code. Further
information on the project is available on the [ZOO Project official
website](http://www.zoo-project.org).

### How does ZOO works ? {#how_does_zoo_works}

ZOO is based on a \'WPS Service Kernel\' which constitutes the ZOO\'s
core system (aka ZOO Kernel). The latter is able to load dynamic
libraries and to handle them as on-demand Web services. The
[ZOOKernel](ZooWebSite : ZooKernel : Introduction "wikilink") is written in C language, but supports several common
programming languages for creating \[ZooWebSite/ZooServices/Introduction
ZOO Services].

A \[ZooWebSite/ZooServices/Introduction ZOO Service] is a link composed
of a ZOO metadata file (.zcfg) and the code for the corresponding
implementation. The metadata file describes all the available functions
which can be called using a WPS Exec Request, as well as the desired
input/output. Services contain the algorithms and functions, and can now
be implemented in C/C++, Fortran, Java, Python, Perl, PHP and
JavaScript.

[ZOOKernel](ZooWebSite : ZooKernel : Introduction "wikilink") works with Apache and can communicate with cartographic engines
and Web mapping clients. It simply adds the WPS support to your spatial
data infrastructure and your Web mapping application. It can use every
GDAL/OGR supported formats as input data and create suitable vector or
raster output for your cartographic engine and/or your web-mapping
client application.

### What are we going to do in this workshop? {#what_are_we_going_to_do_in_this_workshop}

This workshop aims to present the ZOO Project and its features, and to
explain its capabilities regarding the [OGC WPS 1.0.0
specification](http://www.opengeospatial.org/standards/wps). The
participants will learn in 3 hours how to use ZOO Kernel, how to create
ZOO Services and their configuration files and finally how to link the
created Service with a client-side webmapping application. A
pre-compiled ZOO 1.0 version is provided inside OSGeoLive, the OSGeo
official Live DVD. For the sack of simplicity, an OSGeoLive Virtual
Machine image disk is already installed on your computers. This will be
used during this workshop, so the participants won\'t have to compile
and install ZOO Kernel manually. Running and testing ZOO Kernel from
this OSGeoLive image disk is thus the first step of the workshop, and
every participants should get a working ZOO Kernel in less than 30
minutes.

Once ZOO Kernel will be tested from a Web browser using GetCapabilities
requests, participants will be invited to create an OGR based ZOO
Service Provider aiming to enable simple spatial operations on vector
data. Participants will first have to choose whether they will create
the service using C or Python language. Every programming step of the
ZOO Service Provider and the related Services will be each time detailed
in C and Python. Once the ZOO Services will be ready and callable by ZOO
Kernel, participants will finally learn how to use its different
functions from an [OpenLayers](http://www.openlayers.org) simple
application. A sample dataset was providen by Orkney and included in the
OSGeoLiveDVD, data are available trough OGC WMS/WFS WebServices using
[MapServer](http://www.mapserver.org) and will be displayed on a simple
map and used as input data by the ZOO Services. Then, some specific
selection and execution controls will be added in the JavaScript code in
order to execute single and multiple geometries on the displayed
polygons.

Once again, the whole procedure will be organized step-by-step and
detailed with numerous code snippets and their respective explanations.
The instructors will check the ZOO Kernel functioning on each machine
and will assist you while coding. Technical questions are of course
welcome during the workshop.

### Usefull tips for reading : {#usefull_tips_for_reading}

\[\...]\
**Let\'s go !**\
[WorkShop tableof content](ZooWorkshop : FOSS4GJapan "wikilink") \|
[//////////ZooWorkshop/FOSS4GJapan/UsingZooFromOSGeoLiveVMNext](ZooWorkshop : FOSS4GJapan : UsingZooFromOSGeoLiveVMNext "wikilink")

