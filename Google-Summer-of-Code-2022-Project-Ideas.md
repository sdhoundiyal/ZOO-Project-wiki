# ZOO-Community _@_ GSoC _with_ OSGeo

We are floating the project ideas for [ZOO-Project](https://github.com/ZOO-Project/ZOO-Project), [MapMint](https://github.com/mapmint/mapmint) and [MapMint4ME](https://github.com/mapmint/MapMint4ME) projects together at a single wiki page to avoid confusion to the potential contributors. The project ideas are explained in detail below:

_Idea(s):_

## **ZOO-Project**

1. ### Moving the ZOO-Kernel JavaScript support from SpiderMonkey to Node JS

The ZOO-Project is a solid WPS server able to handle services implemented in various different programming languages. The Java bindings have never been tested in advanced configurations and complex data types. The JGrasstools project is a modular processing library and its highly annotated nature makes it possible to adapt quite easily to other toolboxes. One example has been the adaptation to the Geotools Process API. The JGrasstools project, as well as other java based projects (as JTS and even GeoTools) would benefit a lot from the possibility to be used within a WPS environment. The proposal is to bring the Java binding to a mature level and validate them by integrating the JGrasstools libraries. This will allow them to work inside the ZOO-Project and serve its modules under the WPS standard.

**Mentor**: [Gérald Fenoy](https://www.osgeo.org/member/gerald-fenoy/), Aditi Sawant,[Rajat Shinde](https://www.osgeo.org/member/shinde/), 

**Difficulty**: Expert

**Pre-requisites**: Python, JavaScript, C++

**Expected Outcome**: Updated ZOO-Kernel with NodeJS support.

**Time of the project**: 175 or 350 hrs

**Idea in Detail**: We are expecting following deliverables from the project:

-   When the ZOO-Project decided to implement JavaScript in 2009, SpiderMonkey was a well-known technology. Nevertheless, time has changed and now the Node JS implementation is becoming more and more popular over the years.

-   The goal of this GSoC project is to provide an optional V8 support for the ZOO-Kernel. The main goal is to provide a similar implementation to the one already available. So to say, the goal is to provide an implementation which can support the exact same ZOO-Services already existing and implemented using the Node JS framework in place of the current SpiderMonkey implementation.

-   For this purpose, the implementation should be able to load the following JavaScripts files: [ZOO-API](http://zoo-project.org/trac/browser/trunk/zoo-project/zoo-api/js/ZOO-api.js) and [ZOO-prj4js](http://zoo-project.org/trac/browser/trunk/zoo-project/zoo-api/js/ZOO-proj4js.js). The [C functions exposed to the JavaScript language](http://zoo-project.org/trac/browser/trunk/zoo-project/zoo-kernel/service_internal_js.c#L150) should also be available, they are: [alert](http://zoo-project.org/trac/browser/trunk/zoo-project/zoo-kernel/service_internal_js.c#L34), [ZOOTranslate](http://zoo-project.org/trac/browser/trunk/zoo-project/zoo-kernel/service_internal_js.c#L849), [ZOORequest](http://zoo-project.org/trac/browser/trunk/zoo-project/zoo-kernel/service_internal_js.c#L870), [ZOOUpdateStatus](http://zoo-project.org/trac/browser/trunk/zoo-project/zoo-kernel/service_internal_js.c#L955) and [importScripts](http://zoo-project.org/trac/browser/trunk/zoo-project/zoo-kernel/service_internal_js.c#L59).

**Test**: Contributors interested in working on this project idea have to successfully perform the following tasks in the Contributor application period.

-   Test for the understanding of Github (Version Control)

    -   Fork the [ZOO-Project](https://github.com/ZOO-Project/ZOO-Project) Github repository and create a task list in the issues section of the repository.

-   Test for the understanding of Node JS

    -   Prove your understanding of the Node JS framework. The implementation or development is upto the creativity of the contributor.

-   Create a pull request to the [ZOO-Project](https://github.com/ZOO-Project/ZOO-Project) repository with your code.

The link to the Github repository should be mentioned in the final Contributor proposal for the Google Summer of Code 2022.

2. ### Integrating ZOO services with QGIS

The ZOO-Project is a solid WPS server able to handle services implemented in various different programming languages. The Java bindings have never been tested in advanced configurations and complex data types. The JGrasstools project is a modular processing library and its highly annotated nature makes it possible to adapt quite easily to other toolboxes. One example has been the adaptation to the Geotools Process API. The JGrasstools project, as well as other java based projects (as JTS and even GeoTools) would benefit a lot from the possibility to be used within a WPS environment. The proposal is to bring the Java binding to a mature level and validate them by integrating the JGrasstools libraries. This will allow them to work inside the ZOO-Project and serve its modules under the WPS standard.

**Mentor**: [Rajat Shinde](https://www.osgeo.org/member/shinde/), [Gérald Fenoy](https://www.osgeo.org/member/gerald-fenoy/), Aditi Sawant

**Difficulty**: Medium

**Pre-requisites**: Python, JavaScript, QGIS, OGC Standards

**Expected Outcome**: A new way to execute ZOO services from QGIS.

**Time of the project**: 175 or 350 hrs

**Idea in Detail**: We are expecting following deliverables from the project:

-   Using ZOO as a WPS client in QGIS and wrapping the existing algorithms as local processing algorithms directly accessible from QGIS.

**Test**: Contributors interested in working on this project idea have to successfully perform the following tasks in the Contributor application period.

-   Test for the understanding of Github (Version Control)

    -   Fork the [ZOO-Project](https://github.com/ZOO-Project/ZOO-Project) Github repository and create a task list in the issues section of the repository.

-   Test for the understanding of Web Services

    -   Implement and present a short report on working with OGC standardized web services - WMS, WFS and WPS from the QGIS interface

-   Create a pull request to the [ZOO-Project](https://github.com/ZOO-Project/ZOO-Project) repository with your code and report.

The link to the Github repository should be mentioned in the final Contributor proposal for the Google Summer of Code 2022.

## MapMint

1.  ### Adding Cesium support within MapMint

MapMint is a web-based Geographic Information System (GIS), which is designed to facilitate deployment of Spatial Data Infrastructure (SDI). In an SDI, geographic data, metadata, tools, and the users are connected in an interactive manner in a framework so as to use the spatial information in an efficient and flexible way. MapMint combines various different software in a complete and coherent web mapping platform, thus helping users in building their own maps and web-applications. These web-services are built on top of the ZOO-Project. 

**Mentor**: [Rajat Shinde](https://www.osgeo.org/member/shinde/), [Gérald Fenoy](https://www.osgeo.org/member/gerald-fenoy/), Aditi Sawant

**Difficulty**: Medium

**Pre-requisites**: Python, JavaScript, 3D Visualization

**Expected Outcome**: Updated MapMint interface with inbuilt Cesium support.

**Time of the project**: 175 or 350 hrs

**Idea in Detail**: We are expecting following deliverables from the project:

-   In 2021, one of the project ideas (https://wiki.osgeo.org/wiki/GSoC_2021_Implement_3D_scene_visualization_support_using_Potree_and_integrate_with_MapMint) was to implement 3D visualization support inside MapMint dashboard. The objective of this project is to extend it further by enabling Cesium (<https://cesium.com/>) support inside MapMint dashboard.  

**Test**: Contributors interested in working on this project idea have to successfully perform the following tasks in the Contributor application period.

-   Test for the understanding of Github (Version Control)

    -   Fork the[  MapMint](https://github.com/mapmint/mapmint) Github repository and create a task list in the issues section of the repository.

-   Test for the understanding of 3D visualization

    -   Create a sample app visualizing 3D data using Cesium JS library

-   Create a pull request to the MapMint repository with your code.

The link to the Github repository should be mentioned in the final Contributor proposal for the Google Summer of Code 2022.

2. ### Implementing MapMint dashboard based on ZOO services on the Cloud platform

MapMint is a web-based Geographic Information System (GIS), which is designed to facilitate deployment of Spatial Data Infrastructure (SDI). In an SDI, geographic data, metadata, tools, and the users are connected in an interactive manner in a framework so as to use the spatial information in an efficient and flexible way. MapMint combines various different software in a complete and coherent web mapping platform, thus helping users in building their own maps and web-applications. These web-services are built on top of the ZOO-Project. 

**Mentor**:Aditi Sawant, [Gérald Fenoy](https://www.osgeo.org/member/gerald-fenoy/),[  Rajat Shinde](https://www.osgeo.org/member/shinde/)

**Difficulty**: Medium

**Pre-requisites**: Python, JavaScript, 3D Visualization, Azure cloud platform

**Expected Outcome**: Integrated cloud support for the MapMint platform.

**Time of the project**: 175 or 350 hrs

**Idea in Detail**: We are expecting following deliverables from the project:

-   ZOO-Project has been a proud winner of the Microsoft AI for Earth grants. With this project, the idea is to implement the ZOO services stack and algorithms over the Azure cloud and create a containerized setup which could be easy to use and develop.

-   The project would involve implementing MapMint dashboard on the Azure cloud 

**Test**: Contributors interested in working on this project idea have to successfully perform the following tasks in the Contributor application period.

-   Test for the understanding of Github (Version Control)

    -   Fork the[  MapMint](https://github.com/mapmint/mapmint) Github repository and create a task list in the issues section of the repository.

-   Test for the understanding of Azure Cloud

    -   Prove your understanding of the Azure cloud platform. The implementation or development is upto the creativity of the contributor.

-   Create a pull request to the MapMint repository with your code.

The link to the Github repository should be mentioned in the final Contributor proposal for the Google Summer of Code 2022.

## MapMint4ME

1.  ### Implement AR draw support based on OGC ARML standard

MapMint4ME is an android application for the MapMint web service. The android application is built on top of ZOO-Project. ZOO-Project is an open WPS platform. ZOO-Project acts as SDI for the android application and gives users convenience to built their map and application using MapServer and GDAL. The android application MapMint4ME is built on MapMint, so the structure of the data storage and processing is the same, and thus, it is essential to understand the architecture of MapMint. 

**Mentor**: [Rajat Shinde](https://www.osgeo.org/member/shinde/), [Gérald Fenoy](https://www.osgeo.org/member/gerald-fenoy/), Aditi Sawant

**Difficulty**: Expert

**Pre-requisites**: Python, JavaScript, Augmented Reality, OGC Standards

**Expected Outcome**: Updated MapMint4ME app based on OGC ARML standard.

**Time of the project**: 175 or 350 hrs

**Idea in Detail**: We are expecting following deliverables from the project:

-   In 2021, one of the project ideas (https://wiki.osgeo.org/wiki/GSoC_2021_Building_the_AR_Draw_Experience_with_UNITY_3D_and_Integrating_it_with_the_present_MapMint4ME_App) was to implement AR Draw support inside MapMint dashboard using Unity 3D. With this objective, the aim is to explore the implementation based on the OGC ARML 2.0 standard (https://www.ogc.org/standards/arml) for the AR draw support in the MapMint4ME. 

**Test**: Contributors interested in working on this project idea have to successfully perform the following tasks in the Contributor application period.

-   Test for the understanding of Github (Version Control)

    -   Fork the [MapMint4ME](https://github.com/mapmint/MapMint4ME) Github repository and create a task list in the issues section of the repository.

-   Test for the understanding of Web Services

    -   Implement and present a short report on working with OGC standardized web services - WMS, WFS and WPS from the QGIS interface. Read OGC ARML 2.0 standard.

-   Create a pull request to the MapMint4ME repository with your code.

The link to the Github repository should be mentioned in the final Contributor proposal for the Google Summer of Code 2022.

The Contributors are encouraged to reach out to[  Gérald Fenoy](https://www.osgeo.org/member/gerald-fenoy/) and[  Rajat Shinde](https://www.osgeo.org/member/shinde/) for any queries regarding the above-mentioned test. The queries can also be posted to OSGeo SOC mailing list - soc(AT)lists(DOT)osgeo(DOT)org or the [ZOO Project Slack channel](http://zoo-project.slack.com).

_**Apart from this, the best idea is YOUR IDEA. Please feel free to propose your own idea and discuss it with us.**_