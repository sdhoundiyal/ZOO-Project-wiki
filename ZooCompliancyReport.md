## ZOO Project WPS implementation testing {#zoo_project_wps_implementation_testing}

ZOO-PSC would like to report results of tests conducted on ZOO-Kernel
WPS implementation. Comparison of some current WPS implementation was
reported in presentation entitled \"COMPLIANCE TESTING OF OPEN SOURCE
SOFTWARE FOR WEB PROCESSING SERVICES\"
[link](http://www.slideshare.net/TheodorFoerster/compliance-testing-of-open-source-software-for-web-processing-services).

Our testing results are presented in more details below. The test with
ZOO WPS are contrary to the presentation mentioned above
[link](http://www.slideshare.net/TheodorFoerster/compliance-testing-of-open-source-software-for-web-processing-services).
We call upon the authors of the presentation referred above to make
appropriate corrections in their presentation in light of our test
results outlined below. We hope that a more well planned and coordinated
implementation testing can be done in the future.

Gérald Fenoy (Chair ZOO PSC)

## ZOO Project WPS testing details {#zoo_project_wps_testing_details}

In the FOSS4G2010 presentation
[link](http://www.slideshare.net/TheodorFoerster/compliance-testing-of-open-source-software-for-web-processing-services),
some unusual behavior of the ZOO Kernel was pointed out. Hence, the ZOO
PSC decided to conduct our own tests with ZOO WPS implementation using
the same method reported in the FOSS4G2010 presentation.

First note about this response that we have prepared, we weren\'t able
to use XMLSpy 2007 Professional version as no more Evaluation version is
available, so we used the XMLSpy 2011 Professional one as we can use it
for an evaluation period of 30 days.

All the following requests give documents which are valid (using XMLSpy
2011 Professional) against the used schemas.

### GetCapabilities request {#getcapabilities_request}

In the FOSS4G2010 presentation
[link](http://www.slideshare.net/TheodorFoerster/compliance-testing-of-open-source-software-for-web-processing-services),
an error was pointed out about some unexpected metadata : namely Test
attribute to the Metadata node getting the \"Demo\" value. This was due
to wrong ZCFG files of the first Services we made in the beginning of
the 2009 year.

The provided URL to run this test is wrong, the correct one to use is as
below :

<http://zoo-project.org/cgi-bin-new/zoo_loader.cgi?REQUEST=GetCapabilities&SERVICE=WPS&version=1.0.0>

    #html
    <!--
    The annex II linked to this section contains strangely a ProcessDescription document when it shall be a Capabilities Document instead. Maybe we don't have the final version of the report  (at least ZOO-Team hope so).
    -->

So, for the GetCapabilities request, the Capabilities document output by
the ZOO Kernel is **Valid**.

### DescribeProcess request {#describeprocess_request}

It was also reported in the presentation that ZOO Kernel can not handle
the DescribeProcess request and output a valid ProcessDescriptions
Document. Indeed the first versions of ZOO Kernel was wrong in that, but
hopefully the last one, included in OSGeoLiveDVD 4.0 returns already the
valid ProcessDescriptions document.

<http://zoo-project.org/cgi-bin-new/zoo_loader.cgi?REQUEST=DescribeProcess&SERVICE=WPS&version=1.0.0&Identifier=Buffer>

Using the url above we can confirm that ZOO Kernel provide **Valid**
response for the DescribeProcess request.

Note that this request is **Valid** also :

<http://zoo-project.org/cgi-bin-new/zoo_loader.cgi?REQUEST=DescribeProcess&SERVICE=WPS&version=1.0.0&Identifier=Buffer,Boundary,Centroid,ConvexHull,Simplify,Union,Intersection,Difference,SymDifference>

### Execute request {#execute_request}

ZOO WPS provides valid response for Execute as XML POST requests, as it
is the mandatory method.

To use the XML POST requests, please copy/paste from this page, please
follow this [link](http://zoo-project.org/test_services.html) to paste
in the HTML form.

#### Synchronous call using asReference {#synchronous_call_using_asreference}

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 http://schemas.opengis.net/wps/1.0.0/wpsExecute_request.xsd">
    <ows:Identifier>Buffer</ows:Identifier>
    <wps:DataInputs>
    <wps:Input>
    <ows:Identifier>InputPolygon</ows:Identifier>
    <ows:Title>Playground area</ows:Title>
    <wps:Reference xlink:href="http://dreal-official.geolabs.fr/mapjax/webservices/wfs/dreal_lr_general/?VERSION=1.1.0&amp;version=1.0.0&amp;request=GetFeature&amp;typename=Znieff1&amp;maxfeatures=1"/></wps:Input>
    <wps:Input>
    <ows:Identifier>BufferDistance</ows:Identifier>
    <ows:Title>Distance which people will walk to get to a playground.</ows:Title>
    <wps:Data>
    <wps:LiteralData>10</wps:LiteralData>
    </wps:Data>
    </wps:Input>
    </wps:DataInputs>
    <wps:ResponseForm>
    <wps:ResponseDocument storeExecuteResponse="false">
    <wps:Output asReference="true">
    <ows:Identifier>Result</ows:Identifier>
    </wps:Output>
    </wps:ResponseDocument>
    </wps:ResponseForm>
    </wps:Execute>

#### Synchronous call with data included {#synchronous_call_with_data_included}

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 http://schemas.opengis.net/wps/1.0.0/wpsExecute_request.xsd">
    <ows:Identifier>Buffer</ows:Identifier>
    <wps:DataInputs>
    <wps:Input>
    <ows:Identifier>InputPolygon</ows:Identifier>
    <ows:Title>Playground area</ows:Title>
    <wps:Reference xlink:href="http://dreal-official.geolabs.fr/mapjax/webservices/wfs/dreal_lr_general/?VERSION=1.1.0&amp;version=1.0.0&amp;request=GetFeature&amp;typename=Znieff1&amp;maxfeatures=1"/></wps:Input>
    <wps:Input>
    <ows:Identifier>BufferDistance</ows:Identifier>
    <ows:Title>Distance which people will walk to get to a playground.</ows:Title>
    <wps:Data>
    <wps:LiteralData>10</wps:LiteralData>
    </wps:Data>
    </wps:Input>
    </wps:DataInputs>
    <wps:ResponseForm>
    <wps:ResponseDocument storeExecuteResponse="false">
    <wps:Output asReference="false">
    <ows:Identifier>Result</ows:Identifier>
    </wps:Output>
    </wps:ResponseDocument>
    </wps:ResponseForm>
    </wps:Execute>

#### Asynchronous call with data asReference {#asynchronous_call_with_data_asreference}

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 http://schemas.opengis.net/wps/1.0.0/wpsExecute_request.xsd">
    <ows:Identifier>Buffer</ows:Identifier>
    <wps:DataInputs>
    <wps:Input>
    <ows:Identifier>InputPolygon</ows:Identifier>
    <ows:Title>Playground area</ows:Title>
    <wps:Reference xlink:href="http://dreal-official.geolabs.fr/mapjax/webservices/wfs/dreal_lr_general/?VERSION=1.1.0&amp;version=1.0.0&amp;request=GetFeature&amp;typename=Znieff1&amp;maxfeatures=1"/></wps:Input>
    <wps:Input>
    <ows:Identifier>BufferDistance</ows:Identifier>
    <ows:Title>Distance which people will walk to get to a playground.</ows:Title>
    <wps:Data>
    <wps:LiteralData>10</wps:LiteralData>
    </wps:Data>
    </wps:Input>
    </wps:DataInputs>
    <wps:ResponseForm>
    <wps:ResponseDocument storeExecuteResponse="true" status="true">
    <wps:Output asReference="true">
    <ows:Identifier>Result</ows:Identifier>
    </wps:Output>
    </wps:ResponseDocument>
    </wps:ResponseForm>
    </wps:Execute>

Here both statusLocation file and response are **Valid**.

#### Asynchronous call with full data included {#asynchronous_call_with_full_data_included}

You can also use the storeExecuteReponse=\"true\" for ResponseDocument
with the asReference attribute for the Output settled to true as in the
following request :

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 http://schemas.opengis.net/wps/1.0.0/wpsExecute_request.xsd">
    <ows:Identifier>Buffer</ows:Identifier>
    <wps:DataInputs>
    <wps:Input>
    <ows:Identifier>InputPolygon</ows:Identifier>
    <ows:Title>Playground area</ows:Title>
    <wps:Reference xlink:href="http://dreal-official.geolabs.fr/mapjax/webservices/wfs/dreal_lr_general/?VERSION=1.1.0&amp;version=1.0.0&amp;request=GetFeature&amp;typename=Znieff1&amp;maxfeatures=1"/></wps:Input>
    <wps:Input>
    <ows:Identifier>BufferDistance</ows:Identifier>
    <ows:Title>Distance which people will walk to get to a playground.</ows:Title>
    <wps:Data>
    <wps:LiteralData>10</wps:LiteralData>
    </wps:Data>
    </wps:Input>
    </wps:DataInputs>
    <wps:ResponseForm>
    <wps:ResponseDocument storeExecuteResponse="true" status="true">
    <wps:Output asReference="false">
    <ows:Identifier>Result</ows:Identifier>
    </wps:Output>
    </wps:ResponseDocument>
    </wps:ResponseForm>
    </wps:Execute>

The resulting document and the statusLocation document are both
**Valid**.

#### RawDataOutput test {#rawdataoutput_test}

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 http://schemas.opengis.net/wps/1.0.0/wpsExecute_request.xsd">
    <ows:Identifier>Buffer</ows:Identifier>
    <wps:DataInputs>
    <wps:Input>
    <ows:Identifier>InputPolygon</ows:Identifier>
    <ows:Title>Playground area</ows:Title>
    <wps:Reference xlink:href="http://dreal-official.geolabs.fr/mapjax/webservices/wfs/dreal_lr_general/?VERSION=1.1.0&amp;version=1.0.0&amp;request=GetFeature&amp;typename=Znieff1&amp;maxfeatures=1"/></wps:Input>
    <wps:Input>
    <ows:Identifier>BufferDistance</ows:Identifier>
    <ows:Title>Distance which people will walk to get to a playground.</ows:Title>
    <wps:Data>
    <wps:LiteralData>10</wps:LiteralData>
    </wps:Data>
    </wps:Input>
    </wps:DataInputs>
    <wps:ResponseForm>
    <wps:RawDataOutput>
    <ows:Identifier>Result</ows:Identifier>
    </wps:RawDataOutput>
    </wps:ResponseForm>
    </wps:Execute>

The result is valid in the sens that it is a JSON string representing
the resulting polygon.
