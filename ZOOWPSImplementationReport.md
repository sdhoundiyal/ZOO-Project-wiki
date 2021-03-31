## ZOO Project WPS implementation testing {#zoo_project_wps_implementation_testing}

ZOO-PSC would like to report results of tests conducted on ZOO-Kernel
WPS implementation.

Our testing results are presented in more details below. These validity
test have been carried out to ensure that ZOO XML outputs are compliant
to the OGC WPS standerd. It is also an answer to the \"Compliance
testing\" of Open Source WPS implementations presented at FOSS4G2010. We
hope that a coordinated comparison of various WPS implementations can be
done in the near future.

Gérald Fenoy (Chair ZOO PSC)

## ZOO Project WPS testing details {#zoo_project_wps_testing_details}

In light of some unusual behavior of the ZOO Kernel reported, the ZOO
PSC decided to conduct our own tests with ZOO WPS implementation using
the same method reported in the FOSS4G2010 presentation.

First note about this report that we weren\'t able to use XMLSpy 2007
Professional version as no more Evaluation version is available, so we
used the XMLSpy 2011 Professional one as we can use it for an evaluation
period of 30 days.

All the following requests give documents which are valid (using XMLSpy
2011 Professional) against the used schemas.

You can run the tests present in this document using [this bash
script](http://svn.zoo-project.org/trac/attachment/wiki/ZOOWPSImplementationReport/testXmlValidation.sh),
please check for prequistes. It shall give you result like the following
:

    ./testXmlValidation.sh http://zoo-project.org/cgi-bin-new/zoo_loader.cgi
    *Test validity of the answer for GetCapabilities request
    http://zoo-project.org/cgi-bin-new/zoo_loader.cgi?REQUEST=GetCapabilities&SERVICE=WPS validates
    *Test validity of the answer for DescribeProcess requests
    *DescribeProcess for Buffer
    http://zoo-project.org/cgi-bin-new/zoo_loader.cgi?REQUEST=DescribeProcess&SERVICE=WPS&version=1.0.0&Identifier=Buffer validates
    *DescribeProcess for Buffer Boundary Centroid ConvexHull Simplify Union Intersection Difference SymDifference
    http://zoo-project.org/cgi-bin-new/zoo_loader.cgi?REQUEST=DescribeProcess&SERVICE=WPS&version=1.0.0&Identifier=Buffer,Boundary,Centroid,ConvexHull,Simplify,Union,Intersection,Difference,SymDifference validates
    *Test validity of the answer for Execute requests
    ** Test validity of the answer for a synchronous call using asReference
    /tmp/execute_sync_ref.xml validates
    ** Test validity of the answer for a synchronous call with data included
    /tmp/execute_sync_woref.xml validates
    ** Test validity of the answer for an asynchronous call using asReference
    ** 1) Check initial answer
    /tmp/execute_async_ref.xml validates
    ** 2) Check the statusLocation
    http://www.zoo-project.org/zoo/../ms_tmp//ogr_service.zo_21774.xml validates
    ** Test validity of the answer for an asynchronous call with data included
    ** 1) Check initial answer
    /tmp/execute_async_woref.xml validates
    ** 2) Check the statusLocation
    http://www.zoo-project.org/zoo/../ms_tmp//ogr_service.zo_21774.xml validates

You can also consult [this
report](http://zoo-project.org/ZOODEMOREP/demoReport1.html) which is
autogenrated periodically using the same URLs and requests than the one
used in this document.

### GetCapabilities request {#getcapabilities_request}

An error was pointed out about some unexpected metadata : namely Test
attribute to the Metadata node getting the \"Demo\" value. This was due
to wrong ZCFG files of the first Services we made in the beginning of
the 2009 year.

The correct URL to run the test is as below :

<http://zoo-project.org/cgi-bin-new/zoo_loader.cgi?REQUEST=GetCapabilities&SERVICE=WPS&version=1.0.0>

    #html
    <!--
    The annex II linked to this section contains strangely a ProcessDescription document when it shall be a Capabilities Document instead. Maybe we don't have the final version of the report  (at least ZOO-Team hope so).
    -->

So, for the GetCapabilities request, the Capabilities document output by
the ZOO Kernel is **Valid**.

### DescribeProcess request {#describeprocess_request}

ZOO Kernel handle the DescribeProcess request and output a valid
ProcessDescriptions Document. Indeed the first versions of ZOO Kernel
was wrong in that, but hopefully the last one, included in OSGeoLiveDVD
4.0 returns already the valid ProcessDescriptions document.

<http://zoo-project.org/cgi-bin-new/zoo_loader.cgi?REQUEST=DescribeProcess&SERVICE=WPS&version=1.0.0&Identifier=Buffer>

Using the URL above we can confirm that ZOO Kernel provide **Valid**
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

The result is valid in the sense that it is a JSON string representing
the resulting polygon.
