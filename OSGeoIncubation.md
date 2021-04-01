## Incubator Application Questionnaire (ZOO-Project) {#incubator_application_questionnaire_zoo_project}

### 1. Please provide the name and email address of the principal Project Owner. {#please_provide_the_name_and_email_address_of_the_principal_project_owner.}

`   * Gérald FENOY, Chair ZOO PSC, gerald.fenoy@geolabs.fr`

### 2. Please provide the names and emails of co-project owners (if any). {#please_provide_the_names_and_emails_of_co_project_owners_if_any.}

`   * Venkatesh RAGHAVAN raghavan@media.osaka-cu.ac.jp`\
`   * Nicolas BOZON nicolas.bozon@gmail.com`

### 3. Please provide the names, emails and entity affiliation of all official committers {#please_provide_the_names_emails_and_entity_affiliation_of_all_official_committers}

`   * Gérald FENOY (GeoLabs) gerald.fenoy@geolabs.fr`

-   -   Jeff McKenna (Gateway Geomatics)

`   * David SAGGIORATO (Cleolys) david@saggiorato.net`\
`   * Luca DELUCCHI (Fondazioen Edmund Mach) lucadeluge@gmail.com `\
`   * René-Luc D'HONT (3LIZ) rldhont@3liz.com`\
`   * Marco NEGRETTI (Politecnico di Milano) marco.negretti@polimi.it`\
`   * Angelos Tzotsos (National technical university of Athens) gcpp.kalxas@gmail.com`

### 4. Please describe your Project. {#please_describe_your_project.}

ZOO is a WPS (Web Processing Service) open source project released under
a MIT/X-11 style license . It provides an OGC WPS compliant
developer-friendly framework to create and chain WPS Web services. ZOO
is made of three parts:

ZOO Kernel: A powerful server-side C Kernel which makes it possible to
manage and chain Web services coded in different programming languages.

ZOO Services : A growing suite of example Web services based on various
Open Source libraries. (get inspired !)

ZOO API : A server-side JavaScript API able to call and chain the ZOO
Services, which makes the development and chaining processes easier.

### 5. Why is hosting at OSGeo good for your project? {#why_is_hosting_at_osgeo_good_for_your_project}

Hosting the ZOO-Project on the OSGeo server infrastructure is not
planned. If \'Hosting\' means to be \'under the foundation umbrella\'
here, then of course it would be great benefit for the project and will
help it to target a larger audience. It will also probably help the
projects member to promote and spread even more WPS around.

### 6. Type of application does this project represent(client, server, standalone, library, etc.): {#type_of_application_does_this_project_representclient_server_standalone_library_etc.}

WPS Server

### 7. Please describe any relationships to other open source projects. {#please_describe_any_relationships_to_other_open_source_projects.}

Since its inception, ZOO-Project was designed to communicate with the
other OSGeo librairies, and to make them communicate in a standardized
way. The main task of the ZOO- Project is to make OSGeo libraires run on
the server-side as WPS Services.

-   GDAL:

`   GDAL ZOO Services are available for:`\
`   gdalinfo, gdal_grid, gdal_translate, gdal_extractProfile`\
`   ogrinfo, ogr2ogr `

-   MapServer:

`   ZOO-Kernel has an optional support fo MapServer Support (--with mapserver at compil)`\
`   In this case ZOO Kernel is able to spread the ZOO Service results as WMS/WFS/WCS    (write a mapfile on the fly)`

-   GRASS 7.0:

`   ZOO-Kernel is abale to run most of the raster and vector GRASS 7.0 modules (using   WPSBridge library)`

Some other softwares are also supported:

-   R
-   CGAL
-   OpenOffice
-   PyCSW
-   GeoKettle \....

### 8. Please describe any relationships with commercial companies or products. {#please_describe_any_relationships_with_commercial_companies_or_products.}

GeoLabs, Cleolys, Cartogenic and Cartworks (and probably others) are
currently using ZOO-Project for geospatial business and SDI contracts.

ZOO-Project is used by MapMint, an open source based commercial Web GIS
solution powered and edited by Cartoworks Inc (see
<http://www.mapmint.com>)

### 9. Which open source license(s) will the source code be released under? {#which_open_source_licenses_will_the_source_code_be_released_under}

ZOO-Kernel is published under the term of the MIT/X11 open source
licence.

ZOO-Services can contain their own licence term, by now only MIT/X11 is
used.

ZOO-API is published under the term of BSD licence
(\[browser:trunk/zoo-project/zoo-api/js/ZOO-api.js ZOO-api.js\]) and
LGPL (\[browser:trunk/zoo-project/zoo-api/js/ZOO-proj4js.js
ZOO-proj4js.js\]).

### 10. Is there already a beta or official release? {#is_there_already_a_beta_or_official_release}

Yes. ZOO-Project 1.2 is available here :
<http://zoo-project.org/site/Downloads>

### 11. What is the origin of your project (commercial, experimental, thesis or other higher education, government, or some other source)? {#what_is_the_origin_of_your_project_commercial_experimental_thesis_or_other_higher_education_government_or_some_other_source}

`*  Experimental`\
`*  Higher Educations (Universities, thesis)`\
`*  Commercial (companies involved)`

### 12. Does the project support open standards? Which ones and to what extent? (OGC, w3c, ect.) Has the software been certified to any standard (CITE for example)? If not, is it the intention of the project owners to seek certification at some point? {#does_the_project_support_open_standards_which_ones_and_to_what_extent_ogc_w3c_ect._has_the_software_been_certified_to_any_standard_cite_for_example_if_not_is_it_the_intention_of_the_project_owners_to_seek_certification_at_some_point}

Yes. ZOO-Project is based on the Web Processing Service 1.0
specification.

The software wasn\'t certified yet, but we are testing XML validation.

### 13. Is the code free of patents, trademarks, and do you control the copyright? {#is_the_code_free_of_patents_trademarks_and_do_you_control_the_copyright}

Yes, the code is free of patents and trademarks.

ZOO-Kernel is copyrighted by the GeoLabs company

ZOO-Services may include their own copyrights

ZOO-API is copyrighted by the OpenLayers Contributors and the 3LIZ
company

### 14. How many people actively contribute (code, documentation, other?) to the project at this time? {#how_many_people_actively_contribute_code_documentation_other_to_the_project_at_this_time}

`   12 people`

### 15. How many people have commit access to the source code respository? {#how_many_people_have_commit_access_to_the_source_code_respository}

`   6 people`

### 16. Approximately how many users are currently using this project? {#approximately_how_many_users_are_currently_using_this_project}

From 100 to 1000 persons

### 17. What type of users does your project attract (government, commercial, hobby, academic research, etc. )? {#what_type_of_users_does_your_project_attract_government_commercial_hobby_academic_research_etc.}

`*  Government`\
`*  Academic`\
`*  Commercial`

### 18. If you do not intend to host any portion of this project using the OSGeo infrastructure, why should you be considered a member project of the OSGeo Foundation? {#if_you_do_not_intend_to_host_any_portion_of_this_project_using_the_osgeo_infrastructure_why_should_you_be_considered_a_member_project_of_the_osgeo_foundation}

The ZOO-Project is a mature and functionnal open source implementation
of WPS 1.0.0 specifications.

Incubation would help to promote the ZOO-Project to a larger audience
and that will probably attract new contributors to the project.

ZOO-Project is willing to use the other OSGeo softwares trough WPS and
to promote both. WPS is a important field of research in the geospatial
field.

ZOO-Project PSC members are active in the OSGeo activities, FOSS4G, code
sprints and local chapters.

### 19. Does the project include an automated build and test? {#does_the_project_include_an_automated_build_and_test}

Automatic build system is handled by autotools.

A first test suite was integrated for 1.2.0 release including Services
(and Kernel) testing.

### 20. What language(s) are used in this project? (C/Java/perl/etc) {#what_languages_are_used_in_this_project_cjavaperletc}

`*  C/C++`\
`*  Fortran`\
`*  Java`\
`*  Perl`\
`*  Python`\
`*  PHP`\
`*  JavaScript`

### 21. What is the dominant written language (i.e. English, French, Spanish, German, etc) of the core developers? {#what_is_the_dominant_written_language_i.e._english_french_spanish_german_etc_of_the_core_developers}

`*  English`\
`*  French`

### 22. What is the (estimated) size of a full release of this project? How many users do you expect to download the project when it is released? {#what_is_the_estimated_size_of_a_full_release_of_this_project_how_many_users_do_you_expect_to_download_the_project_when_it_is_released}

Size of a release including documentation is approximately 20M.

Expected download per release : 200 - 1000.

