## Bringing pyModis to the web through ZOO-Project {#bringing_pymodis_to_the_web_through_zoo_project}

    #table class="listing"
    {| border=1 class="simple"
    !=Student Name  =
    !Chingchai Humhong 
    |- 
    | =Organization  =
    | [http://www.osgeo.org OSGeo - Open Source Geospatial Foundation]
    |- 
    | =Mentors  =
    | Luca Delucchi and Gerald Fenoy 
    |- 
    | =Title  =
    | Bringing pyModis to the web through ZOO-Project 
    |- 
    | =Sources =
    | [http://zoo-project.org ZOO-Project],[http://www.pymodis.org pyModis]   
    |}

### Brief description of your idea {#brief_description_of_your_idea}

The pyModis project has been developed and used to work with MODIS data,
it provides wxPython user interfaces which are able to download and
process data using [pyModis
scripts](http://www.pymodis.org/scripts/software.html). pyModis depends
on a desktop graphical user interface which does not make it directly
usable from a web application. The idea of this GSoC proposal is to
bring pyModis to the web by publishing Python Web Processing Services
using the ZOO-Project technology accessible through a minimal web
application.

    An idea which can be implemented for the future, based on this initial work, include the creation of new services by combining pyModis, GRASS, OTB and SAGA-GIS services.

### State of the software before GSoC {#state_of_the_software_before_gsoc}

Currently pyModis is able to run on a local computer but cannot be
directly remotely invoked on-demand. ZOO-Project is able to handle
services implemented in the Python language but do not offer any pyModis
capabilities.

### State of the software after GSoC {#state_of_the_software_after_gsoc}

pyModis capabilities will be directly available online, a minimal User
Interfaces will be provided and pyModis services would be able to be
remotely invoked through ZOO-Project using the WPS protocol, so from any
client application providing the WPS capabilities, such as QGIS for
instance.

### Schedule

Prior to the start of the GSoC period, I will learn in more details
every of the involved technologies, starting with ZOO-Project and
pyModis. First, by learning how to write zcfg and Python service should
be implemented for ZOO-Project, then services that use specific pyModis
capabilities. To finish, I will have a deep look in the Hogan templating
system used by the ZOO-Client (part of the ZOO-Project). Having learnt
pyModis scripts in details, I should be able to evaluate the commonly
used data types to be taken into account during the User Interface
design and anticipate the HTML elements to use.

    #table class="listing"
    {| border=1 class="simple"
    !=  Timeline  =
    !=  TODO  =
    !=  Status  =
    |- 
    |   23 – 31 May 2016  
    |  - Starting with ZOO-Project and pyModis by learning how to write ZOO Service Configuration File (ZCFG) and Implementing the Python Service. 
    |   Done  
    |- 
    |   1 – 25 June 2016  
    |  - Implementation of pyModis WPS services corresponding to an available script.<br> - Development made in the ZOO-Project (GRASS, OTB and SAGA processing support) by bringing MODIS data to the web. 
    |   Done  
    |- 
    |   26 June – 10 July 2016  
    |  - Creation of the first version of the template used by the web application to automatically generate the HTML form for accessing pyModis WPS services. 
    |   Done  
    |- 
    |   11 – 25 July 2016  
    |  - Testing template and design user interfaces of web mapping application. 
    |   Done  
    |- 
    |   26 July – 2 August 2016  
    |  - Update the template for the web application to take into account potential new type of input. 
    |   Done  
    |- 
    |   3 –  5 August 2016  
    |  - Usability testing template system and web mapping application. 
    |   Done  
    |- 
    |   6 – 9 August 2016  
    |  - Stringent testing and bug fixes full system. 
    |   Done  
    |- 
    |   10 – 17 August 2016  
    |  - Documenting the web application and publication on the ZOO-Project web site as an example application. 
    |   Done  
    |}

`On the last day of each week, I will write a blog post reporting all the work done during the past week.`

### Reports

#### Week 1 {#week_1}

#### During Bounding period {#during_bounding_period}

-   I have been contacted with my mentors. We discuss to proceed with
    the work to develop something into pyModis and Implementation
    ZOO-Services. I learning introduction to the ZOO-Project and
    pyModis.

#### 1. What did you get done this week? {#what_did_you_get_done_this_week}

-   I installed Ubuntu 14.04.4 LTS on my laptop.
-   I installed pyModis branch 2.0 support also Python 3 follow on
    mentors to recommend.
-   I installed ZOO-Project on web server and ZOO-Kernel linked against
    Python 3.
-   I Starting with ZOO-Project and pyModis by learning how to write ZOO
    Service Configuration File (ZCFG) and Implementing the Python
    Service as images shown below.

#### 2. What do you plan on doing next week? {#what_do_you_plan_on_doing_next_week}

-   Next Week I plan to Implement pyModis WPS services corresponding to
    an available script and made in the ZOO-Project by bringing MODIS
    data to the web.

#### 3. Are you blocked on anything? {#are_you_blocked_on_anything}

-   Right now, I am not blocked on anything, but I think my work is
    quite slow because I do not have experience in using Python.
    Although, I had several difficulties on setting some environments, I
    had solved that. I would like to thanks my mentors (Gérald Fenoy and
    Luca Delucchi) and my advisor Sittichai Choosumrong who helped me to
    solve my problems.

#### Screenshots

    #html
    <center>
    <table style="max-width:75%;margin:0 auto;">
    <tr>
    <td>
    <a href='https://wiki.osgeo.org/wiki/File:Zoo_loader_python3x.JPG' target='_blank'>
     <img src="https://wiki.osgeo.org/images/thumb/f/fc/Zoo_loader_python3x.JPG/800px-Zoo_loader_python3x.JPG" width="320" height="200" alt="" />
     <p><span><center>Test HelloPy Service with Python 3</center></span></p>
    <a>
    </td>
    <td>
    <a href='https://wiki.osgeo.org/wiki/File:Zoo_loader_python2x.JPG' target='_blank'>
     <img src="https://wiki.osgeo.org/images/thumb/a/ac/Zoo_loader_python2x.JPG/320px-Zoo_loader_python2x.JPG" width="320" height="200" alt="" />
      <p><span><center>Test HelloPy Service with Python 2</center></span></p>
    <a>
    </td>
    </tr>
    </table>
    </center>

#### Week 2 {#week_2}

#### 1. What did you get done this week? {#what_did_you_get_done_this_week_1}

This week I have been on the implement pyModis WPS services
corresponding to an available script and made in the ZOO-Project by
bringing MODIS data to the web.

#### 2. What do you plan on doing next week? {#what_do_you_plan_on_doing_next_week_1}

-   Next Week I planning to finish the implementation of pyModis as a
    web service.
-   I will start to test Module to download MODIS as a WPS service.

#### 3. Are you blocked on anything? {#are_you_blocked_on_anything_1}

-   No, but at this moment I have some issue to configuration pyModis to
    working with ZOO-Project.

Below is the link to the branch I am working on
<https://github.com/chingchai/pyModis/tree/gsoc-2016/zoo-pymodis/>

#### Screenshots {#screenshots_1}

#### Week 3 {#week_3}

#### 1. What did you get done this week? {#what_did_you_get_done_this_week_2}

This week I still facing some problems to configuration pyModis to
working with ZOO-Project. The pyModis is inform warnings in ZOO-Service
when execute on web browser \'WxPython missing, no GUI enabled\'. But I
test pyModis WPS Service with ZOO-Kernel linked against Python 2 and
pyModis 1.0.2 It works \[1\]

#### 2. What do you plan on doing next week? {#what_do_you_plan_on_doing_next_week_2}

-   Next Week I planning to configuration GRASS, OTB and SAGA processing
    support in the ZOO-Project by bringing MODIS data to the web.

#### 3. Are you blocked on anything? {#are_you_blocked_on_anything_2}

-   None

Below is the link to the branch I am working on
<https://github.com/chingchai/pyModis/tree/gsoc-2016/zoo-pymodis/>

#### Screenshots {#screenshots_2}

    #html
    <center>
    <table style="max-width:75%;margin:0 auto;">
    <tr>
    <td>
    <a href='https://wiki.osgeo.org/images/a/ab/Modis-testonweb.png' target='_blank'>
     <img src="https://wiki.osgeo.org/images/a/ab/Modis-testonweb.png" width="320" height="200" alt="" />
     <p><span><center>Test downmodis module to download MODIS Data as a WPS Service</center></span></p>
    <a>
    </td>
    <td>
    <a href='https://wiki.osgeo.org/images/b/bd/Modisdown-resul.png' target='_blank'>
     <img src="https://wiki.osgeo.org/images/b/bd/Modisdown-resul.png" width="320" height="200" alt="" />
      <p><span><center>Result downmodis module</center></span></p>
    <a>
    </td>
    </tr>
    </table>
    </center>

#### Week 4 {#week_4}

#### 1. What did you get done this week? {#what_did_you_get_done_this_week_3}

This week I finished downmodis module to download MODIS HDF files from
NASA repository as a WPS service. I have also updated document and code
in GitHub
<https://github.com/chingchai/pyModis/tree/gsoc-2016/zoo-pymodis/>.

#### 2. What do you plan on doing next week? {#what_do_you_plan_on_doing_next_week_3}

-   Next Week I planning to creation of the first version of the
    template used by the web application to automatically generate the
    HTML form for accessing pyModis WPS services.

#### 3. Are you blocked on anything? {#are_you_blocked_on_anything_3}

-   None.

Below is the link to the branch I am working on
<https://github.com/chingchai/pyModis/tree/gsoc-2016/zoo-pymodis/>

#### Screenshots {#screenshots_3}

#### Week 5 {#week_5}

1.  What did you get done this week?

`      This week I finished to create pyModis download and pyModis mosaic as WPS services [1]`

2\. What do you plan on doing next week?

`      Next Week I planning to creation of the template used by the web application to automatically generate the HTML form for accessing pyModis WPS services`

3\. Are you blocked on anything?

`      No`

\[1\]
<https://github.com/chingchai/pyModis/tree/gsoc-2016/zoo-pymodis/pymodis-services/cgi-env/modis>

#### Week 6 {#week_6}

1.  What did you get done this week?

-   This week I have finished to implementation pyModis WPS services,
    there are three services \[1\]:

`      - download data`\
`      - mosaic data`\
`      - convert data`

-   I started working to create the template by use the web application
    to automatically generate the HTML form for accessing pyModis WPS
    services.

2\. What do you plan on doing next week?

-   Next week, I will continue creating the template by use the web
    application to automatically generate the HTML form for accessing
    pyModis WPS services.

3\. Are you blocked on anything?

-   Nothing right now

\[1\]
<https://github.com/chingchai/pyModis/tree/gsoc-2016/zoo-pymodis/pymodis-services/cgi-env/modis>

#### Week 7 {#week_7}

1.  What did you get done this week?

-   This week I continue creating the template by use the web
    application to automatically generate the HTML form for accessing
    pyModis WPS services.
-   I fix the problem about temporarily redirect stdout/stderr of
    convert.modis service

2\. What do you plan on doing next week?

-   Next week, I will continue creating the template by use the web
    application to automatically generate the HTML form for accessing
    pyModis WPS services.
-   Testing template and design user interfaces of web mapping
    application.

3\. Are you blocked on anything?

-   Nothing right now

#### Week 8 {#week_8}

1.  What did you get done this week?

-   This week I continue creating the template by use the web
    application to automatically generate the HTML form for accessing
    pyModis WPS services.
-   Testing template and design user interfaces of web mapping
    application.

2\. What do you plan on doing next week?

-   Next week, I will continue creating the template by use the web
    application to automatically generate the HTML form for accessing
    pyModis WPS services.
-   Testing and update the template for the web application to take into
    account potential new type of input.

3\. Are you blocked on anything?

-   Nothing right now

#### Week 9 {#week_9}

1.  What did you get done this week?

-   This week, I continue creating the template by use the web
    application to automatically generate the HTML form for accessing
    pyModis WPS services.
-   I try to fix pyModis for downloading MODIS data because NASA
    required username and password for download MODIS data. But not
    complete yet.

2\. What do you plan on doing next week?

-   Next week, I will continue creating the template by use the web
    application to automatically generate the HTML form for accessing
    pyModis WPS services.
-   Testing and update the template for the web application.

3\. Are you blocked on anything?

-   No.

#### Week 10 {#week_10}

1.  What did you get done this week?

-   This week, I continue creating the template by use the web
    application to automatically generate the HTML form for accessing
    pyModis WPS services.
-   I try to fix pyModis for downloading MODIS data because the default
    http server \'<http://e4ftl01.cr.usgs.gov>\' has been updated to
    require a NASA earthdata account when downloading files.

2\. What do you plan on doing next week?

-   Next week, I will continue creating the template by use the web
    application.
-   Testing template system and web mapping application.

3\. Are you blocked on anything?

-   No.

#### Week 11 {#week_11}

1.  What did you get done this week?

-   This week, I continue update the template by use the web application
    to automatically generate the HTML form for accessing pyModis WPS
    services.
-   Update service identifier between index.html linked ZCFG file
-   Update require js and edit path mm/zoo_loader.cgi
-   Add WMS Service modis grid and modis point using GeoServer

2\. What do you plan on doing next week?

-   Fix pyModis for download MODIS data.
-   Testing template system and web mapping application.

3\. Are you blocked on anything?

-   No.

#### Week 12 {#week_12}

This is my twelfth report of GSoC: I am working on bringing pyModis to
the web through ZOO-Project.

Brief description of the idea:

-   The pyModis project has been developed and used to work with MODIS
    data, it provides wxPython user interfaces which are able to
    download and process data using pyModis scripts. pyModis depends on
    a desktop graphical user interface which does not make it directly
    usable from a web application. The idea of this GSoC proposal is to
    bring pyModis to the web by publishing Python Web Processing
    Services using the ZOO-Project technology accessible through a
    minimal web application.

The state of the project as it was BEFORE your GSoC:

-   Currently pyModis is able to run on a local computer but cannot be
    directly remotely invoked on-demand. ZOO-Project is able to handle
    services implemented in the Python language but do not offer any
    pyModis capabilities.

The addition that your project brought to the software:

-   By providing pyModis as a service through ZOO-Project, capabilities
    of ZOO-Project will be increased, specially capabilities of python
    in ZOO-Project will be exposed. As a sample web service from this,
    we develop a web service to download, mosaic and convert modis data
    from NASA\'s Land Processes Distributed Active Archive Center (LP
    DAAC) (http://e4ftl01.cr.usgs.gov/). Then, it could be useful to
    whoever that want to download data, mosaic images and convert modis
    data from image to another image file without GIS and Remote Sensing
    knowledge.

Web Site and Document: <https://chingchai.github.io/zoo-pymodis/>

Link to all my commits is available here: GitHub.
<https://github.com/chingchai/pyModis/commits>

Link to the Github:
<https://github.com/chingchai/pyModis/tree/gsoc-2016/zoo-pymodis>

Link to the web application:
<https://github.com/chingchai/pyModis/tree/gsoc-2016/zoo-pymodis/app-service-web/appmodis>

### Student\'s Biography {#students_biography}

#### Programming and GIS {#programming_and_gis}

I am a 28 year-old 2rd year student at the Naresuan University in
Thailand. I am pursuing my Bachelors in Geography and Masters by
research in Geographic Information Science. GIS is my specialization for
research in my Masters. I am looking forward to pursue a career in the
fields with GIS as a core concept. I am interested in open source
development as it is extremely helpful to developers everywhere to
create new and improved programs to solve real world problems. I have
been working on WPS services implementation as a part of my research in
the field of Spatial Informatics and started learning about the
ZOO-Project WPS. After discussing my idea with the ZOO-Project WPS team,
their feedback helped me a lot in refining and redesigning my idea.

#### Computing experience {#computing_experience}

I am quite used to various GIS related softwares like ZOO-Project WPS,
GRASS, QGIS, PostgreSQL/PostGIS, pgRouting, OpenLayers and
OpenStreetMap.

-   **OpenSource GIS:** QGIS, GRASS GIS, gvSIG, uDig, MapWindow GIS,
    Marble, FWTools, GDAL/OGR, GeoServer, MapServer, GeoMoose, GeoNode,
    OpenLayers, PostgreSQL/PostGIS, pgRouting, OSGeo Live, OpenGeoSuite,
    GeoExt and Heron MC.
-   **Operating Systems:** Microsoft Windows and Linux
-   **Programming languages:** HTML, XML, CSS, PHP, JavaScript, Python,
    C++ and SQL

Good Knowledge of Web Mapping Application Development, working knowledge
of computers using spreadsheets and Geospatial Databases system.

#### Research experience {#research_experience}

-   Comparisons of Drainage Network Delineation from Different
    Thresholds of Digital Elevation Models. Geoinfotech 2016, 3-5
    February 2016, Queen Sirikit National Convention Center (QSNCC),
    Bangkok, Thailand.
-   Real-time rainfall Interpolation based on Web Processing Service
    Using FOSS4G and Open Data. FOSS4G-Asia 2014, 2-5 December 2014,
    Asian Institute of Technology, Pathumthani, Thailand.
-   Developing Web-Enabled Considering Decision Support System for Staff
    Dormitory Service in Naresuan University using pgRouting. The 4th
    Conference Geoinformatics Naresuan, 31 October 2014, Naresuan
    University, Phitsanulok, Thailand.
-   A Cloud-Based Platform for Geological Data Acquisition via Mobile
    Device. The 35th Asian Conference on Remote Sensing (ACRS 2014), 27-
    31 October 2014, Nay Pyi Taw, Myanmar.
-   Fall Biomass Assessment in Mea Hong Son Province by Using MODIS
    Data. The 1st Conference Geoinformatics Naresuan, 21 September 2010,
    Naresuan University, Phitsanulok, Thailand.
-   Wild Fire Risk Analysis from Hotspots and Environmental Factors in
    Mae Hong Son Province. GEOINFOTECH 2010 Conference, 15-17 December
    2010, IMPACT Exhibition and Convention Center, Nonthaburi, Thailand.

[OSGeo
wiki](https://wiki.osgeo.org/wiki/Bringing_pyModis_to_the_web_through_ZOO-Project_GSoC_2016)
[Google Summer of Code 2016
Accepted](https://wiki.osgeo.org/wiki/Google_Summer_of_Code_2016_Accepted)
