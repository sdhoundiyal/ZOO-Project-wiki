## Ubuntu 10.04 {#ubuntu_10.04}

-   Ubuntu 10.4 with ZOO Virtual Image

<http://www.zoo-project.org/Ubuntu10.4_ZOO.zip>

1.  root: ZOO.test

## Debian / Ubuntu {#debian_ubuntu}

Tested on Debian Squeeze, Ubuntu 10.04 and Ubuntu 10.10

## Installation workflow {#installation_workflow}

1.  install some dependencies\

sudo apt-get install flex bison libfcgi-dev libxml2 libxml2-dev curl
openssl autoconf checkinstall

1.  download zoo source\

svn checkout <http://svn.zoo-project.org/svn/trunk> zoo-project

1.  install cgic from packages\

cd zoo-project/thirds/cgic206/

1.  change the path of installation\

nano Makefile

-   LIBS=-L./ -lcgic ../fcgi-2.4.0/libfcgi/.libs/libfcgi.a \--\>
    LIBS=/path/to/libfcgi.a
-   cp libcgic.a ../../dist/lib \--\> cp libcgic.a /usr/lib
-   cp cgic.h ../../dist//include \--\> cp cgic.h /usr/include
-   \@echo libcgic.a is in ../../dist/lib and cgic.h is in
    ../../dist//include. \--\> \@echo libcgic.a is in /usr/lib and
    cgic.h is in /usr/include.

1.  compile\

make

1.  install, I prefer use checkinstall for have a simple remove in the
    future\

sudo make install or better sudo checkinstall -D

1.  go to kernel path\

cd ../../zoo-kernel/

1.  create configure file\

autoconf

1.  run configure, in ubuntu 10.04 there isn\'t libmozjs-dev, for use
    js, you can compile SpiderMonkey or use xulrunner-dev package which
    inclue SpiderMonkey, for use the php read
    [ZooKernel/Embed/PHP\#ConfigureandInstallPHPEmbedlibrary](ZooKernel/Embed/PHP#ConfigureandInstallPHPEmbedlibrary "wikilink")\

./configure \--with-java=/path/to/java for use JavaScript with XulRunner
SpiderMonkey you have to edit configure file.

-   JS_CPPFLAGS=\"-I\$JSHOME/include/js\" \--\>
    JS_CPPFLAGS=\"-I\$JSHOME/include\"
-   JS_LDFLAGS=\"-L\$JSHOME/lib -ljs -lm\" \--\>
    JS_LDFLAGS=\"-L\$JSHOME/lib -lmozjs -lm\"
-   JS_LIB=\"js\" \--\> JS_LIB=\"mozjs\"

./configure \--with-js=/usr/lib/xulrunner-devel.1.9.2.n

1.  compile\

make zoo_loader.cgi

1.  copy all the file inside the path of cgi-bin\

sudo cp main.cfg /usr/lib/cgi-bin

sudo cp zoo_loader.cgi /usr/lib/cgi-bin

1.  Install ZOO ServiceProvider\

sudo cp ../zoo-services/hello-py/cgi-env/\*.zcfg /usr/lib/cgi-bin

sudo cp ../zoo-services/hello-py/\*.py /usr/lib/cgi-bin/

1.  change some path in the main.cfg

sudo nano /usr/lib/cgi-bin/main.cfg

-   serverAddress = <http://127.0.0.1>
-   providerSite = <http://127.0.0.1>

1.  try the installation\

<http://127.0.0.1/cgi-bin/zoo_loader.cgi?ServiceProvider=&metapath=&Service=WPS&Request=GetCapabilities&Version=1.0.0>\
<http://127.0.0.1/cgi-bin/zoo_loader.cgi?ServiceProvider=&metapath=&Service=WPS&Request=DescribeProcess&Version=1.0.0&Identifier=HelloPy>\
<http://127.0.0.1/cgi-bin/zoo_loader.cgi?ServiceProvider=&metapath=&Service=WPS&Request=Execute&Version=1.0.0&Identifier=HelloPy&DataInputs=a=myname>

if you have some problem in the execute request add to main.cfg

\[env\]\
PYTHONPATH=`<YOUR_PYTHONPATH>`{=html}
