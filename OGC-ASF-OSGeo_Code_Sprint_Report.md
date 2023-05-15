# OGC-ASF-OSGeo Code Sprint Report

I attended the [OGC-ASF-OSGeo code sprint](https://developer.ogc.org/sprints/20/) from April 25th to 27th in Lausanne, Switzerland. It was an extraordinary and refreshing moment for me to return to the city that hosted the first FOSS4G, which I participated in, organized at that time, 2006, by the same company that has organized this year's code sprint: [CampToCamp](https://www.camptocamp.com/). There is no need to present the company as their contributions to the Open Source community are already well recognized by the community. Returning to a face-to-face code sprint where we can physically meet people was refreshing. We can hug old friends, make new ones, and discover new faces. Also, informal discussions can occur during lunch and dinner, offered by the organizer, right down the great venue's location: [The QG](https://www.openstreetmap.org/way/977563755#map=18/46.54540/6.55026). In addition, several outstanding projects were presented during the opening session. I got the same feeling here: seeing well-established projects and amazing new ones. Participating in this specific code sprint is very appreciative because you have many projects from OGC, OSGeo, and ASF organizations, but not all are Open Source. Nevertheless, as the focus is on Open Standards through the OGC, we can still use these technologies until we support the standard implemented.

After this introduction session, where the software and the standards' evolution presentation occurred, the daily schedule was very convenient. It started with the plan of work from the participant for the day, followed by the work slots, and then we got an end-of-the-day session where participants could show their work results. 

As you are here, it is probably to know what happened during this code sprint about the ZOO-Project specifically. So let's dig into it now.


## ZOO-Project security support update


During the [125th OGC Member meeting](https://www.ogc.org/ogc-events/125th-ogc-member-meeting-dubai/) in Frascati, Italy, I presented the workshop entitled: [ZOO-Project introduction to OGC API - Processes - Part 1: Core Security](https://zoo-project.github.io/workshops/2023/index.html). Indeed, as you already know, the current main branch of the ZOO-Project supports a [new security section](https://zoo-project.github.io/docs/kernel/configuration.html#openapi-security). This security section and the implementation of the filter_in and filter_out services permit handling of the security in your application by providing a way to execute many filters to the requests before they get handed over by the ZOO-Kernel or at the end of the processing pending on the kind of security your service supports. In this [workshop's section](https://zoo-project.github.io/workshops/2023/setup_security_basicauth.html), you can learn how to use the Basic Authentification example service available from the ZOO-Services set. During the code sprint, I focused more on the [OpenID Connect support](https://zoo-project.github.io/workshops/2023/setup_security_openid_connect.html) handled by the Keycloack Identity and Access Management system.

Our purpose was to ensure that users executing a secured process, i.e., HelloPy, cannot be seen by other users when they list the jobs the ZOO-Kernel runs. With the modification we made during the code sprint, the job status information now contains the user's name when the server runs a process. Meaning that internally the ZOO-Kernel can now filter using this username to ensure the validity of the request. 
Per default, the ``anonymous`` username is supposed to be the one used in case of an insecure process. So, in our scenario, all other services are concerned. If not complete, as securing other services would make much sense, it proves that such filtering is possible and illustrates how it helps ensure a secured service provision.
During the code sprint, we created a demonstration instance available online [here](http://tb17.geolabs.fr:8125/ogc-api/). It contains the demonstration interface for our scenario for interacting with the username filtering capability configured. From the associated [swagger-ui](http://tb17.geolabs.fr:8125/swagger-ui/oapip/), you can browse the API to follow how to use the example we have set up for you to review how it works.

First, you should have a GitHub account, which is common enough to expect you to have one already. From the swagger-ui, go down to the /process/HelloPy/execution service endpoint. Click on the green arrow on the right-hand side, then on the lock. At this step, the popup presented in the screenshot below, on the left, should appear. Scroll to the section "BasicAuth (OAuth2, implicit)" as illustrated and enter the following value for the client_id field: ``ZOO-Secured-Client``. Once done, press the green Authorize button to get to the Keycloack demonstration instance. Here, click on GitHub and follow the instructions from your browser to connect using your GitHub account. After you get connected, you should see the second screenshot below on the right. So, you can close the popup by clicking on the cross in the top right corner.

<table>
<tr>
<td>

![Capture d’écran 2023-05-15 à 10 01 48](https://github.com/ZOO-Project/ZOO-Project/assets/1606022/21494930-f874-47f7-a5d8-30f0107a5abf)

</td>
<td>

![Capture d’écran 2023-05-15 à 10 46 09](https://github.com/ZOO-Project/ZOO-Project/assets/1606022/c41b451c-0058-4fd2-9373-c900e4c79f04)

</td>
</tr>
</table>

We defined this secured endpoint (/processes/HelloPy/execution), including only the specific ``respond-async;return=representation`` Prefer header. The HelloPy service invocation can only happen using the asynchronous mode. In reality, it supports all methods, but the OpenAPI configuration makes only this header appear as an option for this secured process. Now that you authenticated with your GitHub account let's try to execute the HelloPy process. To do so, start by clicking on the "Try it out" button, change the default request if needed, then press the big blue Execute button as shown in the screenshot below. Once you have run a process, you are sure that no one else will be able to access its reference from the jobs list. Note that you may have access to more than only your jobs list. As said previously, the anonymous username is used by default, meaning the users appear as if it was unauthenticated. In other words, any authenticated user can access the jobs list to the job identifiers of the service it has run or the unauthenticated user's services. Listing anonymous runs is a requirement, as the user may have access to unsecured processes. In such a case, it should be able also to access these jobs from the jobs list. In our demonstration scenario, only the HelloyPy process execution and the jobs list require authentication. 

![Capture d’écran 2023-05-15 à 13 21 01](https://github.com/ZOO-Project/ZOO-Project/assets/1606022/a7d9647e-d2ba-48a6-aeed-cdf01656afd2)

To ensure that everything goes fine, you can disconnect your user and re-connect with the anonymous user to ensure that you cannot list the job identifier of your test run from the jobs list. Note that with some browsers, you may need to stop and start it again to ensure you are correctly disconnected. Then you can access the jobs list from the swagger-ui and see that your job identifier is not in the returned list.

## ZOO-Project partial part 3 support workflow and chaining

The [OGC API - Processes - Part 3: Workflow and Chaining](https://docs.ogc.org/DRAFTS/21-009.html) draft specification defines multiple conformance classes. We targeted implementing the chaining part during this code sprint, corresponding to the nested and remote processes conformance classes:
http://www.opengis.net/spec/ogcapi-processes-3/0.0/req/nested-processes
http://www.opengis.net/spec/ogcapi-processes-3/0.0/req/remote-core-processes
As we did this using the WPS version 1.0.0 standard, it is possible with these conformance classes to use the result of a process execution as an input of another process execution. So, you can combine multiple process invocations from a single execution request. You have an example below that combines the Buffer and the Centroid process to create buffers of centroids. As it is the case for some time now for our testing, we rely on the [pygeoapi](https://pygeoapi.io) server implementation to access features using the [OGC API - Features - Part 1: Core](https://docs.opengeospatial.org/is/17-069r4/17-069r4.html) specification. The nested process, Centroid, can be easily found. It corresponds to the object with the ``process`` taking the value containing ``Centroid``. The first ``process`` is here to make it easy to remember to a client application what server the process refers to. The ZOO-Kernel does not consider this first parameter. Hence, omitting this parameter would not cause any issues. Also, using another server than the one you are requesting won't imply the remote invocation of another server.

`````
{
    "process": "http://tb17.geolabs.fr:8125/ogc-api/processes/Buffer",
    "inputs": {
	"InputPolygon": {
	    "process": "http://tb17.geolabs.fr:8125/ogc-api/processes/Centroid",
	    "inputs": {
		"InputPolygon": {
		    "href": "https://demo.pygeoapi.io/stable/collections/lakes/items?limit=100&f=json"
		}	
	    },
	    "outputs": {
		"Result": {
		    "format":{
			"mediaType": "application/json"
		    }
		}
	    },
	    "response": "raw"
	},
	"bufferDistance": 0.000000001
    },
    "outputs": {
	"Result": {
	    "format": { "mediaType": "application/json" },
            "transmissionMode": "reference"
	}
    }
}
`````

If we were successful with the implementation before the end of the code sprint, the time was lacking for setting up a new server instance, including this new functionality. Since then, we have put this updated instance in place with this basic implementation of the chaining supported. I still need to look at the result as it seems unusable immediately. But yet, the nested process Centroid result was used as an input for the processing of the primary Buffer service, which was the goal of this implementation.
 

Also, after the implementation provided the expected result, we realized we could not specify that we would like to execute this nested process asynchronously. Even if it would only be an option, we would have wanted to be able to choose between asynchronous and synchronous for nested processes execution. Adding a headers parameter helps define that a nested process should run asynchronously. We were privileged to discuss this with present OGC API - Processes SWG members. The idea is to have a way to define that you are willing to have the nested process run asynchronously. We plan to implement such a capability in upcoming code sprints. We can also imagine a restriction on a process executed with a nested process that requires an asynchronous run to enforce the run of the primary to be asynchronous.


## ZOO-Project OSGeo Incubation

Like any code sprint, meeting real-life participants, sitting together, and discussing important topics are pleasant moments. In our case, we had the privilege to sit and discuss with Tom Kralidis the process of incubating the ZOO-Project as an OSGeo project. We got one ticket down: https://github.com/ZOO-Project/ZOO-Project/issues/39. Tom started the process of election for the OSGeo project officer position https://github.com/ZOO-Project/ZOO-Project/issues/48. A specific discussion about the licensing for the modules included within the ZOO-Project https://github.com/ZOO-Project/ZOO-Project/issues/34. We planned to add a wiki page listing the known deployments https://github.com/ZOO-Project/ZOO-Project/issues/37. Reviewing the current code review again, we noticed that some new files still need to be listed in the code review https://github.com/ZOO-Project/ZOO-Project/issues/38. The discussions were dense and very productive. The work continues on these tasks with the FOSS4G as a target.

## Thanks

Special thanks go to the participants for their great work, the OGC, the OSGeo, and the ASF for organizing the code sprint and to CampToCamp for hosting it.
