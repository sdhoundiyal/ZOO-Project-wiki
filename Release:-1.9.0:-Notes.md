
## ZOO-Project 1.9.0 release notes

This new ZOO-Project release contains new features and fixes.

In November 2021, the Open Geospatial Consortium approved the OGC API - Processes (Part 1: Core) standard. The new ZOO-Project release supports this newly approved version. The MapServer support was integrated with this new standard, even if the output data are only available through WMS, WFS and WCS OGC standards, by now (see [#1](https://github.com/ZOO-Project/ZOO-Project/issues/1)).

### New Features and Fixes

* Update ZOO-Kernel internal messages natural languages po files
* Fix issue with synchronous execution from the HTML UI when requesting something else than raw data output.
* Add support for natural languages to be available within the docker-compose setup.
* Add support for automatic natural languages support.
* Add getValueFromMaps function the C-API to be used from C services requiring to be functional in every memory management mode (load or protected)
* Add support for datetime parameter for jobs filtering as defined in OGC API - Processes.
* Add support for type parameter for jobs filtering as defined in OGC API - Processes.
* Add support for minDuration and maxDuration parameters for jobs filtering as defined in OGC API - Processes.
* Change the table structure for storing ongoing execution status informations to add required field for outputing correct statusInfo.
* Addition in the C-API: function addToMapA, in case there is already a value, then the value is appended to the string and values are coma separated (reason of the change: support for filtering using processId and status in OGC API - Processes).
* Add support for filtering using array of string the jobs list from OGC API - Processes using processId or status parameter
* Change docker-compose to use binary docker image published from GitHub action.
* Minor updates in docker-compose to target the right arch and potentially cross compile in case you run from another arch
* Get back the MapServer automatic publication of outputs/results through OGC Web Services (WMS, WFS, and WCS)
* Update the Basic HTML UI to use the Prefer header in case the execution scenario requires to run the execute request asyncrhonously
* Support the Prefer header for choosing between execution mode scenarios which can be sync/async and raw/document
* Add support for multiple output requested as Raw for OGC API - Processes (why not backport this in WPS?)
* Automatically add the old format of metadata informations to the inputs and outputs to not require a single modification within your existing services
* Update the Basic HTML UI to try to conform to version 1.0-draft.6
* Modify both the request parser and response printer functions from the C-API to conform to version 1.0-draft.6
* Support both the old array of inputs / outputs syntax and the one defined in the draft 1.0-draft.6 (array of inputs for the new syntax may not work as expected)
* Move jobs to root and use /processes/{processID} as execute endpopint
* Make all demos running within docker (including SAGA and OTB)
* Deploy demo HTML UI from github from the Dockerfile
* Add demo ZOO-Services build in the Dockerfile