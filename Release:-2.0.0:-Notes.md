## ZOO-Project 2.0.0 release notes

This new ZOO-Project release contains new features and fixes, listed below.

The ZOO-Project has been accepted as part of the [Docker-Sponsored Open Source Program](https://www.docker.com/community/open-source/application/). You can now find various Docker images with different flavors on [DockerHub](https://hub.docker.com/r/zooproject/zoo-project) under the [ZOO-Project organization](https://hub.docker.com/u/zooproject).

This release introduces the support for [OGC API - Processes - Part 2: Deploy, Replace, Undeploy draft specification](https://docs.ogc.org/DRAFTS/20-044.html) (DRU). You may be interested in the [ZOO-Project-DRU Helm Chart](https://artifacthub.io/packages/helm/zoo-project/zoo-project-dru) published in a dedicated GitHub repository: [ZOO-Project/charts](https://github.com/ZOO-Project/charts) for deploying the solution with the DRU and CWL support on Kubernetes. The [EOEPCA project](https://eoepca.org/) supported the development of the DRU with CWL. The ZOO-Project's HPC support has been updated to enable the **deployment** and execution of Singularity containers on remote HPC. The following [Engineering Report](http://ogc.pages.ogc.org/T19-HPC/documents/D081/document.html#_cf80b896-b3d1-4837-bf52-5cd86b37e734) documents the implementation resulting from the Testbed19 HPGC activity. The ZOO-Project provides a dedicated Docker image named [MDL4EO](https://hub.docker.com/r/zooproject/zoo-project/tags?page=1&name=mdl4eo) with [OTBTF](https://github.com/remicres/otbtf) support (the [original OTBTF Docker image](https://hub.docker.com/u/mdl4eo) proven to be working with the HPC support).


### New Features and Fixes

  * Update relation type to monitor for the status location.
  * Add support for the conformance class remote processes from the
  OGC API - Processes - Part 3: Workflow & chaining. Execution of
  remote processes are automatically run asynchronously in case the
  root process was invoked asynchronously.
  * Parse the Location header from ulinet and the cookie if any.
  * Add schemas to the components and support description stored in the file.
  * Add a trivial DeployOnHpc service for automating the installation
  and the deployment of a singularity container using the image
  parameter provided in the executionUnit used when deploying the
  process.
  * Set the key json_response_object with the JSON response that the
  ZOO-Kernel produced for the request, it can be updated from a
  filter_out process.
  * Update filter_in to support returning a response directly by
  adding a response key in the lenv section (binary is supported for
  this response)
  * Provide an initial Dockefile dedicated to the DRU support with
  remote HPC execution support
  * Add a USE_HPC_NESTEDOUTPUTS build option to activate the nested
  inputs and outputs addition (not supported with OGC API - Processes - Part 1: Core)
  * Update C-API errorException and printExceptionResponse* signatures
  to handle the main configuration maps memory properly  
  *  Build Docker image with DRU supporting OpenEO UDP encoding 
  * Add support for deploying and executing OpenEO User Defined
  Processes by using an OpenEO graph for the executionUnit
  * Add support for schema type string for request body, providing a
  way to include CWL example files in the published OpenAPI
  * Integrate the OGC API - Processes - Part 2: Deploy, Replace,
  Undeploy optional support.
  * Build Docker image based on MDL4EO/OTBTF and the onnx runtime for
  models sharing
  * Integrate the TeamEngine and ETS for OGC API - Processes
  * Add JWT parser in security_service.py as filter_in to allocate
  resources per authenticated user
  * Integrate the work done during GSoC 2022 to support Node.js
  ZOO-Services (cf. updated documentation for NodeJS)
  * Update support to filter the jobs list using the user_id
  * Add support for nested processes n OGC API - Processes - Part 3: 
  Workflows & Chaining
  * Add filter_in and filter_out service array to be invoked previously
  of and after the service run
  * Add trivial support for OpenAPI security, basicAuth / openId, and add
  sample services implementation
  * Add support for MapServer 8.0 (actually 7.7-dev), including
  returning result as OGC API -Features
  * Integrate downloading MapServer 8.0 and building from the
  dedicated Dockerfile-MS8
  * Include basicAuth build instructions in the Dockefile
  * Add basicAuth service illustrating how to secure access to OGC API - Processes using Basic Authentication
  * Use the osecurity section to detect secured path, request method
  from the published OpenAPI
  * Update the printHeaders function to allow Status definition at runtime
  * Add a [osecurity] section to secure access to path, method couple
  from the published OpenAPI
  * Update the database connection handling to make it independent from
  instantiation order
  * Use the RabbitMQ also for OGC API - Processes
  * Pass the subscriber if any is passed from the original request
  * Make C OGR base-vect-ops compatible with memory=protect
  * Add volumes to be shared by the ZOO-Kernel and the ZOO-FPM
  * Add a RabbitMQ and a ZOO-FPM container to docker-compose
  * Add documentation for RabbitMQ support and ZOO Fast Process
  Manager (ZOO-FPM)
  * Optional use of ZOO-Kernel Fast Process Manager backends to handle
  asynchronous execution  
  * Partial integration of the code from the
  Publicamundi_David_integration01-devel branch