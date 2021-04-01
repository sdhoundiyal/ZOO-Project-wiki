## How to install ZOO-Project on MacOS X {#how_to_install_zoo_project_on_macos_x}

Make sure to install
[PROJ](http://www.kyngchaos.com/software/frameworks#proj),
[GEOS](http://www.kyngchaos.com/software/frameworks#geos) and
[GDAL](http://www.kyngchaos.com/software/frameworks#gdal) frameworks.

To install ZOO-Project on your MacOS X computer is to use the following
\[/raw-attachment/wiki/ZooDocumentation/ZOOKernel/MacOSX_installation/ZOO-Project-Installer.pkg
installer\].

You would need also to compile it by yourself for adding some supported
languages or anything else, in this case, please follow instructions
below.

### How to Compile ZOO-Project on MacOS X {#how_to_compile_zoo_project_on_macos_x}

\_\_TOC\_\_

In this page you\'ll find all the required informations to build and run
your ZOO-Kernel using a demo page.

### Requirements

First of all, you\'ll need
[XCode](http://developer.apple.com/technologies/tools/xcode.html).

Before you start downloading ZOO-Project source code, you\'ll need ot
install somme tools required to compile ZOO-Kernel properly.

First of all install PROJ, GEOS and GDAL frameworks from
[here](http://www.kyngchaos.com/software/frameworks).

At this step, you should get the following directories on your local
hard drive :

    #sh
    /Library/Frameworks/PROJ.framework
    /Library/Frameworks/GEOS.framework
    /Library/Frameworks/GDAL.framework

Then, create a `src` directory and download inside [the gettext source
code](http://www.gnu.org/software/gettext/#TOCdownloading) and
uncompress it.

Now, compile gettext with the following commands to produce an universal
binary :

    #sh
    cd gettext-0.18.1.1
    CFLAGS="-O -g -arch i386 -arch ppc -arch x86_64"  \
      LDFLAGS="-arch i386 -arch ppc -arch x86_64"   ./configure
    make
    sudo make install

### Compiling and installing your ZOO-Kernel {#compiling_and_installing_your_zoo_kernel}

Download source from SVN, then use the following command to compile
libcgic :

    #sh
    svn co http://svn.zoo-project.org/svn/trunk zoo
    cd zoo/thirds/cgic206
    make

If you produced the `libcgic.a` file, you can start run `autoconf` and
then `configure` from `zoo-kernel` directory.

    #sh
    cd zoo/zoo-kernel
    autoconf
    ./configure --with-python --with-java=macos \
          --with-gdal-config=/Library/Frameworks/GDAL.framework/Versions/1.7/Programs/gdal-config

Obviously, if you don\'t need Python or Java support then you should
remove the corresponding configure option.

Note that we used `--with-java=macos` configure option. Due to the
generic location on all MacOS X platform of the JDK, you don\'t have to
provide here its full path.

Now, run the following commands to compile and deploy your ZOO-Kernel on
your Apache server :

    #sh
    make
    cp zoo_loader.cgi main.cfg /Library/WebServer/CGI-Executables

You should be ready to request your ZOO-Kernel installation using the
following link :
<http://localhost/cgi-bin/zoo_loader.cgi?request=GetCapabilities&service=WPS>
.

If everything is ok, then you can follow next steps to deploy new
Services Providers.

### Deploy OGR Services Provider {#deploy_ogr_services_provider}

#### Requirements {#requirements_1}

Before your try to use any service, please set correct path in the
main.cfg for `tmpPath` and `tmpUrl`.

You can use the following setup :

    #sh
    tmpPath = /Library/WebServer/Documents/tmp
    tmpUrl = ../../tmp

Obviously you\'ll then need to create this directory, using the
following command :

    #sh
    mkdir /Library/WebServer/Documents/tmp

#### C Version {#c_version}

To compile the base-vect-ops ServicesProvider you\'ll need to edit the
`Makefile` in `zoo/zoo-services/ogr/base-vect-ops/` directory. Add
\"`-I/Library//Frameworks/GEOS.framework/Versions/3/Headers/`\" to the
`CFLAGS` value on the first line. To compile, add GDAL framework to the
`PATH` environmenet variable, to ensure that `gdal-config` tool will be
found, run `make` and then copy `cgi-env` files in the
`/Library/WebServer/CGI-Executables` directory.

    #sh
    cd zoo/zoo-services/ogr/base-vect-ops/
    export PATH=$PATH:/Library/Frameworks/GDAL.framework/Versions/1.7/Programs/
    make
    cp cgi-env/* /Library/WebServer/CGI-Executables

    #html
    <p>
    You can test using this 
    <a href="http://localhost/cgi-bin/zoo_loader.cgi?request=Execute&service=WPS&version=1.0.0&Identifier=Buffer&DataInputs=BufferDistance=1@datatype=interger;InputPolygon=Reference@xlink:href=http%3A%2F%2Fwww.zoo-project.org%3A8082%2Fgeoserver%2Fows%3FSERVICE%3DWFS%26REQUEST%3DGetFeature%26VERSION%3D1.0.0%26typename%3Dtopp%3Astates%26SRS%3DEPSG%3A4326%26FeatureID%3Dstates.15"> url</a>
    if everything is ok with your setup.
    </p>

#### Python Version {#python_version}

#### Requirements {#requirements_2}

First of all run python from a Terminal.app and try the following import
from the python interpreter :

    #python
    import osgeo.ogr
    import libxml2

If you don\'t get any trouble here then that means that you don\'t need
to follow instructions from the next section, else you\'ll need.

##### Install LibXML2 Python Module {#install_libxml2_python_module}

If you get an issue when importing the libxml2 module from your python
interpreter then that mean you need to install the Python support for
the libxml2 library which is already installed on you MacOS X
environment. To accomplish this, you have first to determine what is the
libxml2 installed on your platform, using the following command:

    #sh
    xml2-config --version

Download the source corresponding to your version (i.e. on 10.6.6 you
get 2.7.3) from the libxml2 [download page](ftp://xmlsoft.org/libxml2/)
in src directory then uncompress it.

Use the following command to install the python support :

    #sh
    cd src/libxml2-2.7.3/python/
    python setup.py install

#### Deploy OGR Python Services Provider {#deploy_ogr_python_services_provider}

Now copy the `zoo-services/ogt/base-vect-ops/cgi-env` files into
`/Library/WebServer/CGI-Executables`.

    #html
    <p>
    You can test using this 
    <a href="http://localhost/cgi-bin/zoo_loader.cgi?request=Execute&service=WPS&version=1.0.0&Identifier=BufferPy&DataInputs=BufferDistance=1@datatype=interger;InputPolygon=Reference@xlink:href=http%3A%2F%2Fwww.zoo-project.org%3A8082%2Fgeoserver%2Fows%3FSERVICE%3DWFS%26REQUEST%3DGetFeature%26VERSION%3D1.0.0%26typename%3Dtopp%3Astates%26SRS%3DEPSG%3A4326%26FeatureID%3Dstates.15"> url</a>
    if everything is ok with your setup.
    </p>

### Test using Local Demo Page {#test_using_local_demo_page}

Download the [OpenLayers](http://http://openlayers.org/) library and
uncompress it in your personnal Sites directory (located in your home
directory). Rename the OpenLayers directory as `openlayers`. Download
this
\[/../trac/raw-attachment/wiki/ZooDocumentation/ZOOKernel/MacOSX_installation/zoo-demo.zip
zip archive\] then uncompress it in your personnal Sites directory. Load
your local demo pages using the urls looking like the following
(replacing MyUserName by your MacOS user name) :

-   <http://localhost/~MyUserName/zoo-demo/spatialtools.html>
-   <http://localhost/~MyUserName/zoo-demo/spatialtools-py.html>
