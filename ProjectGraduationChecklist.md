# Project Graduation Checklist

Based on the [OSGeo Project Graduation Checklist version 2.0](https://www.osgeo.org/resources/project-graduation-checklist/).

# Overview

This checklist is based on the ZOO-Project master branch at https://github.com/ZOO-Project/ZOO-Project.

# Incubation Checklist

## Open

The project has demonstrated that it has an open, active and healthy user and developer community:

- [x] Open: projects are expected to function in an open and public manner and include:
- [x] Open source license(s)
   - current license files:
     - ZOO kernel: https://github.com/ZOO-Project/ZOO-Project/blob/main/LICENSE.md
     - all ZOO components: https://github.com/ZOO-Project/ZOO-Project/blob/main/zoo-project/LICENSE
     - the ZOO kernel license at LICENSE.md facilitates license recognition when rendered by GitHub
     - the all ZOO components license at zoo-project/LICENSE contains ALL licenses
 - code: [MIT/X11](https://github.com/ZOO-Project/ZOO-Project/blob/main/LICENSE.md)
 - docs: CC BY 4.0
- [x] Open communication channels,
 - [Mailing list](https://lists.osgeo.org/mailman/listinfo/zoo-project)
 - [Twitter](https://twitter.com/ZOO_Project)
 - [IRC](irc://libera.chat/#zoo-project)
- [x] Open decision making process.
 - A [http://zoo-project.org/docs/contribute/contributors.html?highlight=psc#zoo-project-project-steering-commitee Project Steering Committee] exists which implements https://github.com/ZOO-Project/ZOO-Project/wiki/PSC%3A-process.

- [x] Active and healthy community:
 - [x] The project should have a community of developers and users who actively collaborate and support each other in a healthy way. Eg. collaboration on project activities such as testing, release and feature development.
   - Release processes and guidelines https://zoo-project.github.io/docs/contribute/release.html
   - Bugs and features on GitHub at https://github.com/ZOO-Project/ZOO-Project/issues
   - Discussion in mailing lists and IRC
   - http://zoo-project.org/ZOO-Project/ZOO-Tribe provides an entry point for community engagement
 - [x] Long term viability of the project is demonstrated by showing participation and direction from multiple developers, who come from multiple organizations. Eg. The project is resilient enough to sustain loss of a developer or supporting organisation, often referred to as having a high bus factor. Decisions are made openly instead of behind closed doors, which empowers all developers to take ownership of the project and facilitates spreading of knowledge between current and future team members.
   - There are 11 developers/committers, and 6 active contributors from the following organizations: GeoLabs SARL, Politecnico di Milano, SUPSI, AppTech, Georepublic, Gateway Geomatics, Fondazione Edmund Mach, Osaka City University, and National Technical University of Athens). The very nature of the project provides a kernel and extensible service model that allows for building processes 
   - Various statistics (including number of contributors) for the project can be found at https://www.openhub.net/p/zOO-project
   - Professional support options are provided in https://zoo-project.github.io/docs/contribute/service_providers.html
   - Decisions are made openly via mailing lists/IRC
   - PSC meetings are documented on IRC
   - The project powers OGC API implementation of numerous high profile activities:
     - TODO: https://github.com/ZOO-Project/ZOO-Project/issues/37
   - In support of an inclusive and welcoming community, the code of conduct can always be found at https://github.com/ZOO-Project/ZOO-Project/blob/main/CODE_OF_CONDUCT.md

## Copyright and License

We need to ensure that the project owns or otherwise has obtained the ability to release the project code by completing the following steps:

- [x] All project source code is available under an Open Source license
- [x] Project documentation is available under an open license (e.g. Creative Commons): documentation is licensed as Creative Commons Attribution 4.0 International License
- [ ] The project code, documentation and data has been adequately vetted to assure it is all properly licensed, and a copyright notice (As per a Provenance Review) (TODO: [review https://github.com/ZOO-Project/ZOO-Project/wiki/ProvenanceReview](https://github.com/ZOO-Project/ZOO-Project/issues/38))
- [x] The project maintains a list of all copyright holders identified in the Provenance Review Document: done in https://github.com/ZOO-Project/ZOO-Project/issues/38
- [x]  All code contributors have agreed to abide by the project's license policy, and this agreement has been documented and archived: done at https://github.com/ZOO-Project/ZOO-Project/issues/40

## Processes

- [x] The project has code under configuration management (Eg, subversion, git.)
 - Git: https://github.com/ZOO-Project/ZOO-Project.git
- [x] The project uses an issue tracker and keeps the status of the issue tracker up to date
 - GitHub issues: https://github.com/ZOO-Project/ZOO-Project/issues
- [x] The project has documented its management processes.  This is typically done within a Developers Guide or Project Management Plan.
 - Developer's guide at https://zoo-project.github.io/docs/contribute/code.html
 - Release packaging guide at https://zoo-project.github.io/docs/contribute/release.html
- [x] The project has a suitable open governance policy ensuring decisions are made, documented and adhered to in a public manner. This typically means a Project Management Committee has been established with a process for adding new members. A robust Project Management Committee will typically draw upon developers, users and key stakeholders from multiple organisations as there will be a greater variety of technical visions and the project is more resilient to a sponsor leaving.  ** - A [http://zoo-project.org/docs/contribute/contributors.html?highlight=psc#zoo-project-project-steering-commitee Project Steering Committee] exists which implements https://github.com/ZOO-Project/ZOO-Project/wiki/PSC%3A-process.**
 - [x] The project uses public communication channels for decision making to maintain transparency.  **Yes, mailing list, IRC Channel,and GitHub issue tracker/wiki**.

## Documentation

- [x] The project has user documentation:
 - [x] Including sufficient detail to guide a new user through performing the core functionality provided by the application.
- [x] The project has developer documentation:
 - [x] Including checkout and build instructions. **Yes, see https://zoo-project.github.io/docs/install/index.html**
 - [x] Including commented code, ideally published for developer use. Examples: javadocs for Java applications, or Sphinx documentation for Python: API documentation available at https://zoo-project.github.io/docs/C_API
 - [x] Providing sufficient detail for an experienced programmer to contribute patches or a new module in accordance with the project's programming conventions.  **Yes, see https://zoo-project.github.io/docs/contribute/code.html**

## Release Procedure
In order to maintain a consistent level of quality, the project should follow defined release and testing processes.

- [x] The project follows a defined release process:
 - [x] Which includes execution of the testing process before releasing a stable release
   * Yes, the full release process is documented step-by-step https://zoo-project.github.io/docs/contribute/release.html
   * We are using [GitHub Actions](https://github.com/ZOO-Project/ZOO-Project/actions) for CI testing on commits and pull requests to ensure proper testing and functionality.  Future plans also include addition of the OGC CITE ETA for OGC API - Processes as part of GitHub Actions
- [x] The project follows a documented testing process. Ideally, this includes both automated and manual testing. Ideally this includes documented conformance to set quality goals, such as reporting Percentage Code. 
  - Yes, automated testing through GitHub Actions
  - Manual and automated testing occurs through the OGC-CITE (https://cite.opengeospatial.org) testing
- [x] Release and testing processes provide sufficient detail for an experienced programmer to follow
  * Yes, as noted above

# OSGeo Committees and Community
The OSGeo Foundation is made up of a number of committees, projects and local chapters. This section gathers up information these groups have requested from OSGeo projects. These expectations are not mandatory requirements before graduation, but a project should be prepared to address them in order to be considered a good OSGeo citizen.

## Board

The OSGeo Board holds ultimate responsibility for all OSGeo activities. The Board requests:

- [x] A project provide a Project Officer as primary contact 
 - select a project officer: TODO: [verify via PSC vote](https://github.com/ZOO-Project/ZOO-Project/issues/48)
 - The Project Officer should be listed at Officers and Board of Directors and Contacts
 - This person is established when the incubation committee recommends the project for graduation
 - Your community can change the project officer as needed
 - Add an agenda item to the next board meeting so they can recognise the change of officer.

## Marketing
Access to OSGeo's Marketing_Committee and associated Marketing Pipeline is one of the key benefits of joining the OSGeo foundation. The Marketing Committee requests:

- [x] Marketing artefacts have been created about the project in line with the incubation criteria listed in the OSGeo Marketing Committee's Marketing Artefacts. This lists the documentation requirements for OSGeo-Live. Marketing Artefacts include:
 - Application 
 - Application Quick Start
 - Logo
 - Graphical Image

- [X] Ideally, stable version(s) of executable applications are bundled with appropriate distributions.  In most cases, this will at least include OSGeo-Live, but may also include DebianGIS, UbuntuGIS, and/or osgeo4w, ms4w, etc.)

 - ZOO-Project is part of OSGeoLive, UbuntuGIS and DockerHub.  The project also has promotional / marketing materials (stickers)


## Projects

- [x] Projects do not exist in isolation; and are expected to communicate and collaborate on key issues.

  ZOO-Project works with both upstream (GDAL, PROJ, Rasterio, Shapely, etc. and downstream projects such as EOEPCA and KelFoncier.


## SAC

The System Administration Committee is available to help with infrastructure and facilities. Information for this committee is collected as part of the Project Graduation Checklist.

- The following should be set up:
 - [x] A http://projectname.osgeo.org domain name: **Not requested: the osgeo.org website should link to <https://zoo-project.org>**

- A project may optionally request SAC help to make use 
 - [x] OSGeo issue tracker: **Not requested: issues are managed on [https://github.com/ZOO-Project/ZOO-Project/issues GitHub]**
 - [x] OSGeo mailing list: [exists already](https://lists.osgeo.org/mailman/listinfo/zoo-project)
 - [x] OSGeo svn: **Not requested: source code is managed on [https://github.com/ZOO-Project/ZOO-Project GitHub]**
 - [x] https://downloads.osgeo.org: **Not requested: ZOO-Project releases are made available on [GitHub](https://github.com/ZOO-Project/ZOO-Project/releases)**