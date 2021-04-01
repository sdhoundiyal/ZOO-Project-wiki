## ZooKernel description page {#zookernel_description_page}

On this page you will find everything you need to know about the
ZooKernel.

### Current status {#current_status}

Acutaly, you could compile and use the code available on the svn server
on your own GNU / LINUX platform this way :

#### Requirements

To be able to compile the current source, you need to have some library
allready installed on your system :

-   [FastCGI](http://www.fastcgi.com/drupal/node/5) (installed in
    /path/to/trunk/dist/, using \--prefix=/path/to/trunk/dist configure
    option),
-   \[changeset:15 cgic\] (same, use just `make` from the
    `/path/to/trunk/../third/cgic/` ) .
-   [libxml2](http://www.xmlsoft.org/index.html),
-   [cURL](http://curl.haxx.se/),
-   [Python](http://www.python.org).

#### Getting the source code {#getting_the_source_code}

To get the source code and compile on your platform, use the following
command :

    #sh
    cd zoo/trunk/
    svn checkout svn+ssh://dev.cartography.st/mnt/data3/zoo-project/trunk/zoo-kernel zoo-kernel

#### Compiling the source code {#compiling_the_source_code}

First of all, you\'ll need to edit the Makefile and uncomment
\"`-DLINUX_FREE_ISSUE`\" on the first line, then use the following
commands :

    #sh
    cd zoo-kernel
    make
    make zoo_loader.cgi
    make demo_service.zo

Now, you get the ZooKernel (Shell and Cgi version) and two \"service
providers\" of different kind : `demo_service.zo` (C++) and
`test_service.py` (Python), now use them together.

#### Using the code {#using_the_code}

##### From the command line {#from_the_command_line}

To run request with ZooKernel from command command line, use the
following example :

    #sh
    ./service_loader ./ test_service.zo GetCapabilities
    ./service_loader ./Buffer.zcfg test_service.zo DescribeProcess
    ./service_loader ./Buffer.zcfg ./demo_service.zo Execute helloworld
    ./service_loader ./Buffer.zcfg ./demo_service.zo Execute printAgrument 1 2
    ./service_loader ./Buffer.zcfg ./demo_service.zo Execute printAgrument 1 2 bg
    PYTHONPATH=. ./service_loader ./Distance.zcfg test_service Execute helloworld

Using ZOO Kernel from the command line is very usefull in development
phase, this way you don\'t have to publish a not working ZOO Service
Provider to test and check your service. It can be also useful for ZOO
Kernel debuging purpose.

##### From an apache web server {#from_an_apache_web_server}

You could use the cgi version of zoo_loader on your own apache server.
Do do this, use the following instruction.

Copy the cgi script, the demo service and the required files in your
`cgi-bin` directory.

    #sh
    cp /path/to/trunk/zoo-kernel/zoo_loader.cgi /var/www/localhost/cgi-bin
    cp /path/to/trunk/zoo-services/demo/demo_service.zo /var/www/localhost/cgi-bin/test_service.zo
    cp /path/to/trunk/zoo-services/*/cgi-bin/*zcfg /var/www/localhost/cgi-bin
    cp /path/to/trunk/zoo-kernel/*cfg /var/www/localhost/cgi-bin

Create a file called `.htaccess` in a zoo directory from the directory
index of your apache instalaltion.

    #sh
    cat > /var/www/localhost/htdocs/zoo/.htaccess << EOF
      RewriteEngine on
      RewriteCond %{REQUEST_FILENAME} !-f
      RewriteCond %{REQUEST_FILENAME} !-d
      RewriteCond %{DOCUMENT_ROOT}/%{REQUEST_FILENAME} !=%{DOCUMENT_ROOT}/login.php
      RewriteRule (.*)/(.*)/(.*) /cgi-bin/zoo_loader.cgi?ServiceProvider=$2&metapath=$1 [L,QSA]
      RewriteRule (.*)/(.*)/ /cgi-bin/zoo_loader.cgi?ServiceProvider=$2&metapath=$1 [L,QSA]
      RewriteRule (.*)/(.*) /cgi-bin/zoo_loader.cgi?ServiceProvider=$1&metapath= [L,QSA]
    EOF

Then you have to request your installation using your favorite browser.
For instance, this
[link](http://127.0.0.1/zoo/test_service.zo/?Service=WPS&Request=GetCapabilities&Version=1.0.0)
should work from your Apache web server.

You could also see the Cgi Version from [Shilpa
!](http://shilpa.media.osaka-cu.ac.jp/zoo/?Service=WPS&request=GetCapabilities&Version=1.0.0)

Some samples requests running on the Shilpa server (using KVP requests)
:

-   DescribeProcess samples :
    -   [Buffer](http://shilpa.media.osaka-cu.ac.jp/zoo/?Service=WPS&Request=DescribeProcess&Version=1.0.0&Language=en-CA&Identifier=Buffer)
    -   [Distance](http://shilpa.media.osaka-cu.ac.jp/zoo/?Service=WPS&Request=DescribeProcess&Version=1.0.0&Language=en-CA&Identifier=Distance)
    -   [Multiply](http://shilpa.media.osaka-cu.ac.jp/zoo/arithmetics/wps/?Service=WPS&Request=DescribeProcess&Version=1.0.0&Language=en-CA&Identifier=Multiply)
    -   [Gdal_Translate](http://shilpa.media.osaka-cu.ac.jp/zoo/driftx/wps/?Service=WPS&Request=DescribeProcess&Version=1.0.0&Language=en-CA&Identifier=Gdal_Translate)
    -   [Distance,Buffer](http://shilpa.media.osaka-cu.ac.jp/zoo/?Service=WPS&Request=DescribeProcess&Version=1.0.0&Language=en-CA&Identifier=Distance,Buffer)
-   Execute samples :
    -   Arithmetics Service Provider :
        -   [Execute Sample for Multiply
            Identifier](http://shilpa.media.osaka-cu.ac.jp/zoo/arithmetics/wps/?request=Execute&service=WPS&version=1.0.0&language=en-CA&Identifier=Multiply&DataInputs=A=12@datatype=integer;B=10@datatype=integer&ResponseDocument=Result).
    -   Basic GDAL Service Provider :
    -   [Using Gdal_Translate to convert a GeoTiff datasource to an
        AAIGrid
        datasource](http://shilpa.media.osaka-cu.ac.jp/zoo/driftx/wps/?request=Execute&service=WPS&version=1.0.0&language=en-CA&Identifier=Gdal_Translate&DataInputs=Format=AAIGrid@datatype=string;InputDSN=srtm_kashiwara@datatype=string;OutputDSN=demo007@datatype=string).
    -   [Using Gdal_Translate to crop a GeoTiff datasource and
        potentialy convert datasource
        format](http://shilpa.media.osaka-cu.ac.jp/zoo/driftx/wps/?request=Execute&service=WPS&version=1.0.0&language=en-CA&Identifier=Gdal_Translate&DataInputs=Format=JPEG@datatype=string;InputDSN=srtm_kashiwara@datatype=string;OutputDSN=demo007@datatype=string)
    -   [Use an xlink:href
        value](http://shilpa.media.osaka-cu.ac.jp/zoo/driftx/wps/?request=Execute&service=WPS&version=1.0.0&language=en-CA&Identifier=Gdal_Translate&DataInputs=Format=GIF@datatype=string;InputDSN=srtm_kashiwara@datatype=string;OutputDSN=srtm_kashiwara_output6@datatype=string;ProjWin=135.6212504,34.5820833,135.6679170,34.5670833,urn:ogc:def:crs:EPSG:6.6:4326,2;demo=Reference@xlink:href=http%3A%2F%2Fexamples.oreilly.com%2Fwebmapping%2Fch7%2Fairports.gml)
        [(this is the used
        url)](http://examples.oreilly.com/webmapping/ch7/airports.gml)
    -   [Use a WFS Request as an xlink:href
        valur](http://shilpa.media.osaka-cu.ac.jp/zoo/driftx/wps/?request=Execute&service=WPS&version=1.0.0&language=en-CA&Identifier=Gdal_Translate&DataInputs=Format=GIF@datatype=string;InputDSN=srtm_kashiwara@datatype=string;OutputDSN=srtm_kashiwara_output6@datatype=string;ProjWin=135.6212504,34.5820833,135.6679170,34.5670833,urn:ogc:def:crs:EPSG:6.6:4326,2;demo=Reference@xlink:href=http%3A%2F%2Fcarto.languedoc-roussillon.ecologie.gouv.fr%2Fwebservices%2Fwfs%2Fdiren_general%2F%3FVERSION%3D1.1.0%26service%3DWFS%26request%3DGetFeature%26typename%3DZnieff1%26maxfeatures%3D1)
        [(the WFS request
        used)](http://carto.languedoc-roussillon.ecologie.gouv.fr/webservices/wfs/diren_general/?VERSION=1.1.0&service=WFS&request=GetFeature&typename=Znieff1&maxfeatures=1).
        See [here](ApacheErrorLog "wikilink") to see
        maps data structure extracted from the apache error log
        correspoding to this request)
    -   Basic OGR Service :
    -   The WKS (Well Known Service :) ) Buffer Operation :
        -   [Sample using
            ResponseDocument](http://shilpa.media.osaka-cu.ac.jp/zoo/?request=Execute&service=WPS&version=1.0.0&Identifier=Buffer&DataInputs=BufferDistance=100@datatype=interger@uom=meter;InputPolygon=Reference@xlink:href=http%3A%2F%2Fcarto.languedoc-roussillon.ecologie.gouv.fr%2Fwebservices%2Fwfs%2Fdiren_general%2F%3FVERSION%3D1.1.0%26service%3DWFS%26request%3DGetFeature%26typename%3DZnieff1%26maxfeatures%3D1&ResponseDocument=BufferedPolygon)
            using a xlink:href [WFS
            query](http://carto.languedoc-roussillon.ecologie.gouv.fr/webservices/wfs/diren_general/?VERSION=1.1.0&service=WFS&request=GetFeature&typename=Znieff1&maxfeatures=1)
            URL-Encoded as a DataInputs value
        -   [Same sample using
            lineage](http://shilpa.media.osaka-cu.ac.jp/zoo/?request=Execute&service=WPS&version=1.0.0&Identifier=Buffer&DataInputs=InputPolygon=Reference@xlink:href=http%3A%2F%2Fcarto.languedoc-roussillon.ecologie.gouv.fr%2Fwebservices%2Fwfs%2Fdiren_general%2F%3FVERSION%3D1.1.0%26service%3DWFS%26request%3DGetFeature%26typename%3DZnieff1%26maxfeatures%3D1;BufferDistance=100@datatype=interger@uom=meter&ResponseDocument=BufferedPolygon&Lineage=true)
            (usefull to display the data).
        -   [Sample using
            RawDataOutput](http://shilpa.media.osaka-cu.ac.jp/zoo/?request=Execute&service=WPS&version=1.0.0&Identifier=Buffer&DataInputs=BufferDistance=100@datatype=interger@uom=meter;InputPolygon=Reference@xlink:href=http%3A%2F%2Fcarto.languedoc-roussillon.ecologie.gouv.fr%2Fwebservices%2Fwfs%2Fdiren_general%2F%3FVERSION%3D1.1.0%26service%3DWFS%26request%3DGetFeature%26typename%3DZnieff1%26maxfeatures%3D1&RawDataOutput=BufferedPolygon)
            using a xlink:href the same WFS query URL-Encoded as a
            DataInputs value than the first one
    -   [Distance](http://shilpa.media.osaka-cu.ac.jp/zoo/?request=Execute&service=WPS&version=1.0.0&Identifier=Distance&DataInputs=InputEntity1=Reference@xlink:href=http%3A%2F%2Fcarto.languedoc-roussillon.ecologie.gouv.fr%2Fwebservices%2Fwfs%2Fdiren_general%2F%3FVERSION%3D1.1.0%26service%3DWFS%26request%3DGetFeature%26typename%3DZnieff1%26maxfeatures%3D1;InputEntity2=Reference@xlink:href=http%3A%2F%2Fcarto.languedoc-roussillon.ecologie.gouv.fr%2Fwebservices%2Fwfs%2Fdiren_general%2F%3FVERSION%3D1.1.0%26service%3DWFS%26request%3DGetFeature%26typename%3DZnieff2%26maxfeatures%3D1)
    -   [GetArea](http://shilpa.media.osaka-cu.ac.jp/zoo/?request=Execute&service=WPS&version=1.0.0&Identifier=GetArea&DataInputs=InputEntity1=Reference@xlink:href=http%3A%2F%2Fcarto.languedoc-roussillon.ecologie.gouv.fr%2Fwebservices%2Fwfs%2Fdiren_general%2F%3FVERSION%3D1.1.0%26service%3DWFS%26request%3DGetFeature%26typename%3DZnieff1%26maxfeatures%3D1;BufferDistance=100@datatype=interger@uom=meter)
    -   [ConvexHull](http://shilpa.media.osaka-cu.ac.jp/zoo/?request=Execute&service=WPS&version=1.0.0&Identifier=ConvexHull&DataInputs=InputPolygon=Reference@xlink:href=http%3A%2F%2Fcarto.languedoc-roussillon.ecologie.gouv.fr%2Fwebservices%2Fwfs%2Fdiren_general%2F%3FVERSION%3D1.1.0%26service%3DWFS%26request%3DGetFeature%26typename%3DZnieff1%26maxfeatures%3D1;BufferDistance=100@datatype=interger@uom=meter)
    -   [Boundary](http://shilpa.media.osaka-cu.ac.jp/zoo/?request=Execute&service=WPS&version=1.0.0&Identifier=Boundary&DataInputs=InputPolygon=Reference@xlink:href=http%3A%2F%2Fcarto.languedoc-roussillon.ecologie.gouv.fr%2Fwebservices%2Fwfs%2Fdiren_general%2F%3FVERSION%3D1.1.0%26service%3DWFS%26request%3DGetFeature%26typename%3DZnieff1%26maxfeatures%3D1;BufferDistance=100@datatype=interger@uom=meter)
    -   Python samples :
    -   [HelloPy](http://demo.zoo-project.org/zoo/?request=Execute&service=WPS&version=1.0.0&Identifier=HelloPy&DataInputs=a=Your%20Name%20Here@datatype=string)
    -   Java samples :
    -   [HelloWorldJava](http://demo.zoo-project.org/zoo/wps/?request=Execute&service=WPS&version=1.0.0&language=en-CA&Identifier=HelloWorldJava&DataInputs=S=Venkatesh%20Raghavan@datatype=string&ResponseDocument=Result)
    -   Fortran samples :
    -   [hellof](http://demo.zoo-project.org/zoo/?request=Execute&service=WPS&version=1.0.0&Identifier=hellof&DataInputs=S=Your%20Name%20Here@datatype=string)

Some sample (using POST XML requests), to use those examples you will
have to put the following XML documents in the textare on [this
page](http://shilpa.media.osaka-cu.ac.jp/demo/test_services_post1.html),
then press \"run using XML Request\" to see the ZooKernel process your
query :

-   A simple GetCapabilities request :

    #xml
    <wps:GetCapabilities xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 ../wpsGetCapabilities_request.xsd" language="en-CA" service="WPS">
        <wps:AcceptVersions>
            <ows:Version>1.0.0</ows:Version>
        </wps:AcceptVersions>
    </wps:GetCapabilities>

-   A simple DescribeProcess request :

    #xml
    <DescribeProcess xmlns="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 ../wpsDescribeProcess_request.xsd" service="WPS" version="1.0.0" language="en-CA">
    <ows:Identifier>Buffer</ows:Identifier>
    <ows:Identifier>Boundary</ows:Identifier>
    <ows:Identifier>GetArea</ows:Identifier>
    </DescribeProcess>

-   A sample Execute request using ResponseDocument (same as previous
    example using Buffer from basic ogr service) :

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0
    ../wpsExecute_request.xsd">
        <ows:Identifier>Buffer</ows:Identifier>
        <wps:DataInputs>
            <wps:Input>
                <ows:Identifier>InputPolygon</ows:Identifier>
                <ows:Title>Playground area</ows:Title>
                <wps:Reference xlink:href="http://carto.languedoc-roussillon.ecologie.gouv.fr/webservices/wfs/diren_general/?VERSION=1.1.0&amp;service=WFS&amp;request=GetFeature&amp;typename=Znieff1&amp;maxfeatures=1"/>
            </wps:Input>
            <wps:Input>
                <ows:Identifier>BufferDistance</ows:Identifier>
                <ows:Title>Distance which people will walk to get to a playground.</ows:Title>
                <wps:Data>
                    <wps:LiteralData>400</wps:LiteralData>
                </wps:Data>
            </wps:Input>
        </wps:DataInputs>
        <wps:ResponseForm>
            <wps:ResponseDocument>
                <wps:Output>
                    <ows:Identifier>BufferedPolygon</ows:Identifier>
                    <ows:Title>Area serviced by playground.</ows:Title>
                    <ows:Abstract>Area within which most users of this playground will live.</ows:Abstract>
                </wps:Output>
            </wps:ResponseDocument>
        </wps:ResponseForm>
    </wps:Execute>

-   A sample Execute request using RawData (same as previous example
    using Buffer from basic ogr service) :

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0
    ../wpsExecute_request.xsd">
        <ows:Identifier>Buffer</ows:Identifier>
        <wps:DataInputs>
            <wps:Input>
                <ows:Identifier>InputPolygon</ows:Identifier>
                <ows:Title>Playground area</ows:Title>
                <wps:Reference xlink:href="http://carto.languedoc-roussillon.ecologie.gouv.fr/webservices/wfs/diren_general/?VERSION=1.1.0&amp;service=WFS&amp;request=GetFeature&amp;typename=Znieff1&amp;maxfeatures=1"/>
            </wps:Input>
            <wps:Input>
                <ows:Identifier>BufferDistance</ows:Identifier>
                <ows:Title>Distance which people will walk to get to a playground.</ows:Title>
                <wps:Data>
                    <wps:LiteralData>400</wps:LiteralData>
                </wps:Data>
            </wps:Input>
        </wps:DataInputs>
        <wps:ResponseForm>
            <wps:RawDataOutput>
                <ows:Identifier>BufferedPolygon</ows:Identifier>
            </wps:RawDataOutput>
        </wps:ResponseForm>
    </wps:Execute>

-   A sample using two different kind of entities (GML reference and
    JSON String) :

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0
    ../wpsExecute_request.xsd">
            <ows:Identifier>Union</ows:Identifier>
            <wps:DataInputs>
                    <wps:Input>
                            <ows:Identifier>InputEntity1</ows:Identifier>
                            <wps:Reference xlink:href="http://carto.languedoc-roussillon.ecologie.gouv.fr/webservices/wfs/diren_general/?VERSION=1.1.0&amp;service=WFS&amp;request=GetFeature&amp;typename=Znieff1&amp;maxfeatures=1"/>
                    </wps:Input>
                    <wps:Input>
                            <ows:Identifier>InputEntity2</ows:Identifier>
                            <wps:Data>
                            <wps:ComplexData mimeType="application/json">
    {"type":"Polygon","coordinates":[[[-102.036758,36.988972],[-106.860657,36.989491],[-109.047821,36.996643],[-109.055199,38.24493],[-109.052864,39.518196],[-109.050591,40.210545],[-109.047638,40.998474],[-107.918037,41.00341],[-104.051201,41.003227],[-102.620789,41.000225],[-102.047279,40.998077],[-102.04557,40.697323],[-102.036758,36.988972]]]}
                            </wps:ComplexData>
                            </wps:Data>
                    </wps:Input>
            </wps:DataInputs>
            <wps:ResponseForm>
                    <wps:ResponseDocument>
                            <wps:Output>
                                    <ows:Identifier>Result</ows:Identifier>
                            </wps:Output>
                    </wps:ResponseDocument>
            </wps:ResponseForm>
    </wps:Execute>

-   same Union sample using 2 embedded JSON Strings :

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0
    ../wpsExecute_request.xsd">
            <ows:Identifier>Union</ows:Identifier>
            <wps:DataInputs>
                    <wps:Input>
                            <ows:Identifier>InputEntity1</ows:Identifier>
                            <wps:Data>
                            <wps:ComplexData mimeType="application/json">
    {"type":"Polygon","coordinates":[[[-102.036758,36.988972],[-106.860657,36.989491],[-109.047821,36.996643],[-109.055199,38.24493],[-109.052864,39.518196],[-109.050591,40.210545],[-109.047638,40.998474],[-107.918037,41.00341],[-104.051201,41.003227],[-102.620789,41.000225],[-102.047279,40.998077],[-102.04557,40.697323],[-102.036758,36.988972]]]}
                            </wps:ComplexData>
                            </wps:Data>
                    </wps:Input>
                    <wps:Input>
                            <ows:Identifier>InputEntity2</ows:Identifier>
                            <wps:Data>
                            <wps:ComplexData mimeType="application/json">
    {"type":"Polygon","coordinates":[[[-102.036758,36.988972],[-106.860657,36.989491],[-109.047821,36.996643],[-109.055199,38.24493],[-109.052864,39.518196],[-109.050591,40.210545],[-109.047638,40.998474],[-107.918037,41.00341],[-104.051201,41.003227],[-102.620789,41.000225],[-102.047279,40.998077],[-102.04557,40.697323],[-102.036758,36.988972]]]}
                            </wps:ComplexData>
                            </wps:Data>
                    </wps:Input>
            </wps:DataInputs>
            <wps:ResponseForm>
                    <wps:RawDataOutput>
                            <wps:Output>
                                    <ows:Identifier>Result</ows:Identifier>
                            </wps:Output>
                    </wps:RawDataOutput>
            </wps:ResponseForm>
    </wps:Execute>

