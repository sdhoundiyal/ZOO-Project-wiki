## ZooKernel Installation Guide {#zookernel_installation_guide}

On this page you will find informations about how to compile and use ZOO
Kernel with your Apache web server.

### Requirements

To be able to compile the current ZOO Kernel, you need to have some
libraries allready availlable on your system :

-   [FastCGI](http://www.fastcgi.com/drupal/node/5) (installed in
    /path/to/trunk/dist/, using \--prefix=/path/to/trunk/dist configure
    option),
-   \[browser:/trunk/cgic cgic\] (same, use just `make` from the
    `/path/to/trunk/../third/cgic/` ) .
-   [libxml2](http://www.xmlsoft.org/index.html),
-   [cURL](http://curl.haxx.se/),
-   [OpenSSL](http://www.openssl;org),
-   [Python](http://www.python.org),
-   [PHP Embedded](http://www.php.net) (optional, see [compilations
    notes](http://trac.zoo-project.org/wiki/ZooKernel/Embed/PHP#ConfigureandInstallPHPEmbedlibrary)),
-   \[Java SDK\] (optional),
-   [SpiderMonkey](http://www.mozilla.org/js/spidermonkey/) (optional)

#### Getting the source code {#getting_the_source_code}

To get the source code and compile on your platform, use the following
command :

    #sh
    cd zoo/
    svn checkout svn+ssh://dev.cartography.st/mnt/data3/zoo-project/trunk/ trunk

Now you get your local copy of the official ZOO svn server.

### Compilation

#### GNU/Linux

ZOO Kernel use Autotools, to compile the ZOO Kernel just use the
following command (please use `./configure --help` to get more
informations about options) :

    #sh
    cd trunk/zoo-kernel
    ./configure --with-js=/usr/ --with-gdal-config=/usr/bin/gdal-config --with-php=/usr/lib/php5.2.10/ --with-java=no
    make zoo_loader.cgi

#### WIN32

ZOO Kernel can be compiled on WIN32 platforms using [Microsoft Visual
C++ Express Edition 2008](http://www.microsoft.com/express/Windows/)
this way (please note that you should probably edit the makefile.vc file
to suit your needs) :

    #sh
    cd trunk/zoo-kernel
    nmake /f makefile.vc zoo_loader.cgi

### Install ZOO Kernel and ZOO ServiceProvider {#install_zoo_kernel_and_zoo_serviceprovider}

Suppose that your Apache server handle cgi-scripts located in
`/var/www/localhost/cgi-bin`. You should copy the `zoo_loader.cgi`
script in this directory as the `main.cfg` file (see bellow).

    #sh
    # Install your ZOO Kernel
    cp main.cfg /var/www/localhost/cgi-bin
    cp zoo_loader.cgi /var/www/localhost/cgi-bin
    # Install your ZOO ServiceProvider :
    cp ../zoo-services/hello-py/cgi-env/*.zcfg /var/www/localhost/cgi-bin
    cp ../zoo-services/hello-py/*.py /var/www/localhost/cgi-bin/

The main configuration file, `main.cfg`, contains configuration
parameters (in the `main` section) which can be accessed from your
service (using the `main_cfg` parameter) or by the ZOO Kernel (for
instance, we set that `env` is for the automaticaly setting of
environement variable), and metadata.

You should edit the main configuration file before running yoru first
request to your ZOO Kernel.

### Apache ZOO .htaccess {#apache_zoo_.htaccess}

From your Apache `DocumentRoot`, create and fill a file called
`.htaccess` in a `zoo` directory, using the following command.

    #sh
    mkdir /var/www/localhost/htdocs/zoo/
    cat > /var/www/localhost/htdocs/zoo/.htaccess << EOF
      RewriteEngine on
      RewriteCond %{REQUEST_FILENAME} !-f
      RewriteCond %{REQUEST_FILENAME} !-d
      RewriteCond %{DOCUMENT_ROOT}/%{REQUEST_FILENAME} !=%{DOCUMENT_ROOT}/login.php
      RewriteRule (.*)/(.*)/(.*) /cgi-bin/zoo_loader.cgi?ServiceProvider=$2&metapath=$1 [L,QSA]
      RewriteRule (.*)/(.*)/ /cgi-bin/zoo_loader.cgi?ServiceProvider=$2&metapath=$1 [L,QSA]
      RewriteRule (.*)/(.*) /cgi-bin/zoo_loader.cgi?ServiceProvider=$1&metapath= [L,QSA]
    EOF

### Testing

Run first requests to your ZOO Kernel installation :

    http://my.website/zoo/?Service=WPS&Request=GetCapabilities&Version=1.0.0
    http://my.website/zoo/?Service=WPS&Request=DescribeProcess&Version=1.0.0&Identifier=HelloPy
    http://my.website/zoo/?Service=WPS&Request=Execute&Version=1.0.0&Identifier=HelloPy&DataInputs=a=My%20Name@dataType=string

You are ready to go now, developing your own services following the
ZOODeveloperGuide.

