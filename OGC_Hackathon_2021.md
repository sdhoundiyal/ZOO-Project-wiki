# OGC Code Sprint 2021 Report

From June 8th to 10th I got the privilege to meet and work with a group of amazing people from different countries and, working for different companies, all gathered to work on the OGC API - Processes specification and make it the best we can.

On day-to-day basis, the code sprint was starting by a 1h session where people got the opportunity to share ideas, visions, current status of Client and Server implementations, many constructive discussions happened, demos were presented and people express their feelings about the current status of the specifications. The same session occurred mid-day and then at the end of the day. In between, we had time to update our implementation depending on the latest discussion, have discussion with other participants in the Code Sprit, try to see where there can be improvement, if any.

In comparison with the last OGC Code Sprint in London where I was participating, I should say that the main difference was, well for me, the time difference 😄  but hopefully, I did not have to run to my flight this time and can attend the closing session entirely this time.

Ok, right, this is not very useful in a report but hey, remember I am human being here and I slowly recover from the jet lag after no travelling 😃 

On the draft specification side, a lots of progresses has been made, PR has been applied to the draft specification and, some modifications has been presented, discussed and reviewed. We had an amazingly fast iterative adaptation of both clients and servers over the three days.

After this short overview of how great was the workshop, let's now come back to the specific ZOO-Project implementation which is probably the reason why you are on this page.

## ZOO-Project OGC API - Processes updated server implementation

The code sprint was the occasion for me to try to get our implementation as up-to-date as possible with the last draft of the specification. A special focus has been put on trying to implement a solution to the `"response":"raw"` when multiple output are outputed and the client don't request for any specific output. Indeed, with the new specification this is now possible and now possible from the ZOO-Kernel too. On this other hand, having this implemented made me realized that there may be some issue to first store this kind of output and return them to the client in a way or another. This is under discussion at the SWG level and once the decision will be taken, it will be implemented within the ZOO-Kernel implementation.

I have added the capability to provide examples within the OpenAPI that is generated by the ZOO-Kernel based on your configuration files (`main.cfg` and `oas.cfg`). Actually this new capability simply requires few lines to be added to the òas.cfg` file to configure the examples that are static json files available with the source code. Not much code added but still, what is nice doing so is that, the OpenApi accessed from [swagger-ui](http://tb17.geolabs.fr:8091/swagger-ui/oapip/) provided direct usable execute request body that are ready to use. 

## ZOO-Project OGC API - Processes updated demonstration UI

The code sprint was the occasion for me to rebirth the very Basic HTML UI we were providing with the previous version of the specification. Now, it has been updated and works right out of the box, simply install the last version th way you use usually then, you are ready to interact with the ZOO-Project OGC API - Processes tentative implementation server. No need that for fast testing purpose, you may use the docker-compose setup. A special thanks goes to Samuel Souk-Aloun to have introduced it few months back.

This code (both HTML and JavaScript) is not a reference in any case, it is simply here to illustrate how one can quickly setup a primitive User Interface that would interact with an OGC API - Processes implementation.

As before, this Basic HTML UI is generated by a WPS service execution that takes in input a single parameter name tmpl that will take the server path you are accessing. Bellow there are two different WPS 1.0.0 execute request to access the same content in different format.

* [The UI within the ExeucteRequest](http://tb17.geolabs.fr:8091/cgi-bin/zoo_loader.cgi?service=WPS&service=WPS&request=Execute&version=1.0.0&Identifier=display&ResponseDocument=Result&DataInputs=tmpl=@xlink:href=http://tb17.geolabs.fr:8091/ogc-api/)
* [The UI as RawDataOutput](http://tb17.geolabs.fr:8091/cgi-bin/zoo_loader.cgi?service=WPS&service=WPS&request=Execute&version=1.0.0&Identifier=display&RawDataOutput=Result&DataInputs=tmpl=@xlink:href=http://tb17.geolabs.fr:8091/ogc-api/) (not usable due to some links issue within the HTML code)
* [Basic HTML UI](http://tb17.geolabs.fr:8091/ogc-api/)

As you can see by accessing from the [Landing Page](http://tb17.geolabs.fr:8091/ogc-api/) to the [Processes list](http://tb17.geolabs.fr:8091/ogc-api/processes.html) that the UI has been slightly updated, I mean, DataTable was added giving the user the capability of filtering the processes.

A good start exemple to play with can be this process exposed by the [SAGA-GIS](http://www.saga-gis.org/) OpenSource platform: [Pythagoras' Tree](http://tb17.geolabs.fr:8081/ogc-api/processes/SAGA.garden_fractals.1.html). From this last page, click on RESULT (which is the single output for this service) then, set transmission to reference (to get a link rather than the full bunch of data which may be huge). Click the submit button, a window appear where you can see the requestBody to be sent to the server. By clicking on submit job, you should see a loading bar appearing and showing you the current status of the execution then at then end of the execution, hopefully you will get a response providing a URL to your result. Which in this case will be a Pythagoras’ tree.

In case you want to change a bit the parameters, ANGLE should gets values in the `[0,90]` interval and, MINSIZE in the `[0.001,100]`. You probably ask to yourself: "but why is he providing such informations when the OGC API - Processes should return this information precisely?". Well, I would say that I discovered this mistake/omission when writing this report. Note that with the previous version of the specification the server was providing such kind of informations and, I will fix that in to coming days.

Obviously, once you get the simple (in the sense that it does not require any geographic data as input, so you won't have to wonder if you provided the right format or have to search for any file to run testing) example working, you can try other services in the same way. Please, in case you face any failure with the HTML Basic UI or, one or more processes you are trying to use. Then, please report back by filling an [issue](https://github.com/ZOO-Project/ZOO-Project/issues/new) and we will try to fix it as soon as possible.

**Special thanks go to following OpenSource softwares (amongst others): [OrfeoToolBox](https://www.orfeo-toolbox.org/), [SAGA-GIS](http://www.saga-gis.org/) and [GDAL](https://gdal.org/) and their developpers. Without them, the list of services and the processing capability offered may have been reduced to nothing**








 