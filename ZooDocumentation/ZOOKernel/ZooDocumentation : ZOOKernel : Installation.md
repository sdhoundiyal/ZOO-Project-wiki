## Compilation

[TOC()](TOC() "wikilink")

This page provides documentation on how to compile then install
ZOO-Kernel on Unix and Win32 platforms.

IMPORTANT: more detailed notes you can [find
here](http://zoo-project.org/docs/kernel/installation.html#kernel-installation).

### Unix

For Unix users, ZOO-Kernel comes with a GNU autoconf \"configure\"
script that should take care of (hopefully!) all compilation issues for
you.

The configure script won\'t work on Windows. See section \[\#WIN32
WIN32\] for details on compiling on Windows systems.

#### For the impatient {#for_the_impatient}

ZOO requires a third party program, the CGI program. To build
`zoo_loader.cgi` CGI program with the default options, go to the default
options, go to the directory where you extracted the ZOO-Kernel source
code package and use the following command:

    #sh
     $ cd thirds/cgic206
     $ make
     $ cd ../../zoo-project/zoo-kernel
     $ ./configure
     $ make

Unless something went wrong, you should have executables in the current
directory for the zoo_loader.cgi CGI program. You can copy the
zoo_loader.cgi program and the main.cfg file to your HTTP server\'s CGI
directory and start using it.

At this step your ZOO-Kernel should work. Nevertheless, don\'t forget to
correct the main.cfg settings to set tmpPath and tmpUrl to fit your web
server configuration.

#### configure options {#configure_options}

Here is the list of available options as returned by
`./configure --help`:

    #sh
      --with-gdal-config=FILE specify an alternative gdal-config file
      --with-xml2config=FILE  specify an alternative xml2-config file
      --with-python=PATH      To enabled python support or specify an alternative
                              directory for python installation, disabled by
                              default
      --with-php=PATH         To enabled php support or specify an alternative
                              directory for php installation, disabled by default
      --with-perl=PATH        To enabled perl support or specify an alternative
                              directory for perl installation, disabled by default
      --with-java=PATH        To enabled java support, specify a JDK_HOME,
                              disabled by default
      --with-js=PATH          specify --with-js=path-to-js to enabled js support,
                              specify --with-js on linux debian like, js support
                              is disabled by default

All the options are described in more details below.

#### (Required) GDAL Support: {#required_gdal_support}

If your gdal-config program is not found in your PATH then you can use
the \"\--with-gdal-config\" option to speficy its location. For
instance, let suppose that your gdal-config was installed in
/usr/local/bin and this directory is not in your PATH, then you can use
the following command:

    #sh
     $ ./configure --with-gdal-config=/usr/local/bin/gdal-config

#### (Required) XML2 Support: {#required_xml2_support}

If your xml2-config program is not found in your PATH then you can use
the \"\--with-xml2config\" option to specify its location. For instance,
let suppose that your xml2-config was installed in /usr/local/bin end
this directory is not in you PATH, then you can use the following
command:

    #sh
     $ ./configure --with-xml2config=/usr/local/bin/xml2-config

#### (Optional) Python Support {#optional_python_support}

If you want to activate the Python Support for ZOO-Kernel then you will
have to use the \"\--with-python\" option. If your python-config program
is found in your PATH then you don\'t have to specify the path where
Python was installed, so using the following command:

    #sh
     $ ./configure --with-python

This suppose that python-config is found in your PATH.

In case your python-config is not found in your PATH, then you can set
the Python installation directory you are using. For instance, let
suppose that you installed Python in /usr/local, then you can use the
following command:

    #sh
     $ ./configure --with-python=/usr/local

This suppose that /usr/local/bin/python-config exists.

#### (Optional) PHP Support {#optional_php_support}

To be able to activate PHP Support for ZOO-Kernel you\'ll need to get a
local PHP Embedded installation, for more informations about configure
options to use to get such kind of PHP installation you can refer to
this page :

`              `[`http://zoo-project.org/trac/wiki/ZooKernel/Embed/PHP`](http://zoo-project.org/trac/wiki/ZooKernel/Embed/PHP)` `

If you want to activate the PHP Support for ZOO-Kernel then you will
have to use the \"\--with-php\" option. If your php-config program is
found in your PATH then you don\'t have to specify the path where PHP
was installed, so using the following commnd:

    #sh
     $ ./configure --with-php

This suppose that php-config is found in your PATH.

In case your php-config is not found in your PATH, then you can set the
PHP installation directory you are using. For instance, let suppose that
you installed PHP in /usr/local, then you can use the following command:

    #sh
     $ ./configure --with-php=/usr/local

This suppose that /usr/local/bin/php-config exists.

#### (Optional) Perl Support {#optional_perl_support}

If you want to activate the Perl Support for ZOO-Kernel then you will
have to use the \"\--with-perl\" option. If you do not set any value to
this option, then perl program will be searched in your PATH. So in such
case, you can use the following command:

    #sh
     $ ./configure --with-perl 

This suppose that perl is found in your PATH.

In other case, for custom Perl installation, you can set the
installation directory. For instance, let suppose that you installed
Perl in /usr/local and /usr/local/bin is not in your PATH, then you can
use the following command:

    #sh
     $ ./configure --with-perl=/usr/local

This suppose that /usr/local/bin/perl exists.

#### (Optional) Java Support {#optional_java_support}

If you want to activate the Java Support for ZOO-Kernel then you will
have to use the \"\--with-java\" option and set the installation path of
your Java SDK. For instance, let suppose that your Java SDK was
installed in /usr/lib/jvm/java-6-sun-1.6.0.22/ directory, then you can
use the following command:

    #sh
     $ ./configure --with-java=/usr/lib/jvm/java-6-sun-1.6.0.22/

This suppose that the include/linux and jre/lib/i386/client/
subdirectories exist in /usr/lib/jvm/java-6-sun-1.6.0.22/, include/linux
contains the jni.h headers file and jre/lib/i386/client/ contains the
libjvm.so file.

Note that on MacOS X you only have to set macos as value for the
\"\--with-java\" option to get the Java Support for ZOO-Kernel
activated. So using the following command:

    #sh
     $ ./configure --with-java=macos

#### (Optional) JavaScript Support {#optional_javascript_support}

If you want to activate the JavaScript Support for ZOO-Kernel then you
will have to use the `--with-js` option. If you are using a
\"Debian-like\" GNU/Linux distribution then dpkg will be used to detect
if the required packages was installed and you don\'t have to specify
anything here, so you can use the following command:

    #sh
     $ ./configure --with-js 

This suppose that `js_api.h` and `libmozjs.so` are found in default
directories.

If you get a custom installation of SpiderMonkey or you are not using a
Debian packaging system, then you\'ll have to specify the directory
where you installed it. For instance, let suppose that you installed
your SpiderMonkey in `/usr`, then you\'ll have to use the following
command:

    #sh
     $ ./configure --with-js=/usr

This suppose that the `/usr/include/js` exists and contains the
`js_api.h` headers file and `/usr/lib` contains `libmozjs.so` file.

### WIN32

#### Requirements

ZOO-Kernel on WIN32 platform requires the following for building:

-   OSGeo4W packages : Apache, gdal, Python
-   libfcgi
-   libcrypto, flex + bison (installed in a directory we call `TPATH`)

To be able to access flex and bison tools, you should use the following
command :

    #sh
    set TPATH=c:\My\Install\Directory
    set PATH=%PATH%;%TPATH%\bin

To make sure that environnement variables are correctly set for
compilation, use the following command :

    #sh
    c:\Program Files\Microsoft Visual Studio 9.0\VC\bin\vcvars32.bat

#### libcgic

Make sure you get the file `C:\OSGeo4W\lib\libfcgi.lib` on your
computer, then you can run the following commands to build the required
libcgic:

    #sh
    cd thirds/cgic206
    make

#### Build and deploy ZOO-Kernel {#build_and_deploy_zoo_kernel}

To build ZOO-Kernel you should first edit the nmake.opt file to set the
following variables :

-   -   `LIBINTL_CPATH`: the libintl installation path
    -   `PYTHON_CPATH`: the python installation path
    -   `TPATH`: discussed \[\#Requirements before\]
    -   `GEODIR`: OSGeo4W installation path
    -   `CFLAGS`: flags used at compilation time
    -   `LDFLAGS`: flags used at link time

Then, run the following commands to build your own WIN32 ZOO-Kernel:

    #sh
    cd zoo-kernel
    nmake /f makefile.vc

To make sure your build can run you need to copy it in the bin directory
from the OSGeo4W installation path, then try to run it from command
line:

    #sh
    copy zoo_loader.cgi main.cfg c:\OSGeo4W\bin
    cd c:\OSGeo4W\bin
    .\zoo_loader.cgi "request=GetCapabilities&service=WPS"

If everything went right running from command line, then you can run it
from your browser and build services.

#### Build and deploy ServicesProvider {#build_and_deploy_servicesprovider}

Actually only few ServiceProvider was tested on WIN32 platform. To
compile a service provider called SP you should run the following
commands:

    #sh
    cd zoo-service\SP
    nmake /f makefile.vc

As this `makefile.vc` uses `nmake.opt` you modified earlier, it should
succeed.

Now you just need to copy files from the `cgi-env` directory into
`c:\OSGeo4W\bin` to deploy your ServiceProvider (should contain at least
a `.zo` and a `.zcfg`).
