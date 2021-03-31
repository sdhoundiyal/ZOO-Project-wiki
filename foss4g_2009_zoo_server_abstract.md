## FOSS4G ZOO Presentation Abstract {#foss4g_zoo_presentation_abstract}

Here is the content I\'ve sent today on the official foss4g2009 web
site.

### Name

Gérald Fenoy

### Email

gerald.fenoy\@geolabs.fr

### Organisation

GeoLabs SARL

### About you {#about_you}

GeoLabs SARL owner.

Two authors for this presentation :

-   Gérald Fenoy, Geolabs SARL
-   Nicolas Bozon, 3LIZ SARL

### Title

ZOO project : an open WPS Platform

### Abstract

The ZOO Project was born to provide a technical solution to the online
geoprocessing needs encountered by the GeoLabs and 3LIZ companies. The
ZOO platefrom is made of two parts : ZOO server, a WPS compliant C++
engine, and ZOO client which is a JSON based javascript API built on top
of OpenLayers.

The ZOO server is based on a « WPS Service Kernel » which constitutes
the ZOO core system. It is able to dynamicaly load on demand various
kind of services. A service could be view as a couple composed by a
metadata file and the code for the corresponding implentation. The
metadata file decribes all functions(s) which have to be callable using
a WPS Exec Request. Services could be easily implemented in C++, Python
or Perl and contains the functions of the service. Services developers
should be able to implement services easily in their favorite langages
without having to take care about formats of inputs and outputs for
instance, storing results, this will be directly done by the WPS Service
Kernel.

The ZOO client is a JSON based javascript API designed to communicate
with ZOO server using a GeoJSON proxy to make use of ZOO Server
input/ouptut only with Javascript and Mapserver.

### Tags

wps server service oriented architecture modular approach geoprocessing
service creation metadata json based web client
