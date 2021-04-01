## openSUSE

Zoo-Kernel is maintained as a package in [OpenSUSE Build Service
(OBS)](https://build.opensuse.org/package/show?package=zoo-kernel&project=Application%3AGeo).
This way, rpm\'s are provided for all versions of openSUSE Linux (11.2,
11.3, 11.4, Factory).

### Stable Releases {#stable_releases}

For installing Zoo-Kernel in openSUSE there are 3 ways available:

#### One Click Installer {#one_click_installer}

One-click installer that can be found
[here](http://software.opensuse.org/search?q=zoo-kernel&baseproject=openSUSE%3A11.4&lang=en&exclude_debug=true).
For openSUSE 11.4 this is the direct
[link](http://software.opensuse.org/ymp/Application:Geo/openSUSE_11.4/zoo-kernel.ymp?base=openSUSE%3A11.4&query=zoo-kernel)

#### Yast Software Manager using a GUI {#yast_software_manager_using_a_gui}

The
[Application:Geo](http://download.opensuse.org/repositories/Application:/Geo/)
repository has to be added to the Software Repositories and then
Zoo-kernel can be found in Software Management through search.

#### Command line (as root for openSUSE 11.4) {#command_line_as_root_for_opensuse_11.4}

    zypper ar http://download.opensuse.org/repositories/Application:/Geo/openSUSE_11.4/
    zypper refresh
    zypper install zoo-kernel

#### Try the installation {#try_the_installation}

<http://localhost/cgi-bin/zoo_loader.cgi?ServiceProvider=&metapath=&Service=WPS&Request=GetCapabilities&Version=1.0.0>\
<http://localhost/cgi-bin/zoo_loader.cgi?ServiceProvider=&metapath=&Service=WPS&Request=DescribeProcess&Version=1.0.0&Identifier=HelloPy>\
<http://localhost/cgi-bin/zoo_loader.cgi?ServiceProvider=&metapath=&Service=WPS&Request=Execute&Version=1.0.0&Identifier=HelloPy&DataInputs=a=myname>

### Unstable Version {#unstable_version}

The latest development version of ZOO-Kernel can be found in OBS under
the project
[home:tzotsos](https://build.opensuse.org/project/show?project=home%3Atzotsos).
ZOO-Kernel packages are maintained and tested there before being
released to the Application:Geo repository.

Installation methods are identical as the stable version. Make sure to
use [this](http://download.opensuse.org/repositories/home:/tzotsos/)
repository instead.

#### Command line installation (as root for openSUSE 11.4) {#command_line_installation_as_root_for_opensuse_11.4}

    zypper ar http://download.opensuse.org/repositories/home:/tzotsos/openSUSE_11.4/
    zypper refresh
    zypper install zoo-kernel
    zypper install zoo-kernel-grass-bridge

Additionally, there is the option of adding the zoo-wps-grass-bridge
package. This option will automatically install grass7 (svn trunk).

