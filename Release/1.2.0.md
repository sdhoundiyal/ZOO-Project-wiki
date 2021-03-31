[TOC](TOC "wikilink")

### ZOO-Project version 1.2.0 {#zoo_project_version_1.2.0}

[Release Notes](http://zoo-project.org/trac/wiki/Release/1.2.0/Notes)

#### Download

#### Archives

-   **ZOO-Project Release 1.2.0:
    \[/raw-attachment/wiki/Release/1.2.0/zoo-project-1.2.0.tar.bz2
    zoo-project-1.2.0.tar.bz2\] \|
    \[/raw-attachment/wiki/Release/1.2.0/zoo-project-1.2.0.zip
    zoo-project-1.2.0.zip\]**
-   ZOO-Project Release 1.2.0-rc1:
    \[/raw-attachment/wiki/Release/1.2.0/zoo-project-1.2.0-rc1.tar.bz2
    zoo-project-1.2.0-rc1.tar.bz2\] \|
    \[/raw-attachment/wiki/Release/1.2.0/zoo-project-1.2.0-rc1.zip
    zoo-project-1.2.0-rc1.zip\]
-   ZOO-Project Release 1.2.0-rc2:
    \[/raw-attachment/wiki/Release/1.2.0/zoo-project-1.2.0-rc2.tar.bz2
    zoo-project-1.2.0-rc2.tar.bz2\] \|
    \[/raw-attachment/wiki/Release/1.2.0/zoo-project-1.2.0-rc2.zip
    zoo-project-1.2.0-rc2.zip\]
-   ZOO-Project Release 1.2.0-rc3:
    \[/raw-attachment/wiki/Release/1.2.0/zoo-project-1.2.0-rc3.tar.bz2
    zoo-project-1.2.0-rc3.tar.bz2\] \|
    \[/raw-attachment/wiki/Release/1.2.0/zoo-project-1.2.0-rc3.zip
    zoo-project-1.2.0-rc3.zip\]

#### Subversion

-   **ZOO-Project Release 1.2.0:
    <http://svn.zoo-project.org/svn/tags/rel-1.2.0>**
-   ZOO-Project Release 1.2.0-rc1:
    <http://svn.zoo-project.org/svn/tags/rel-1.2.0-rc1>
-   ZOO-Project Release 1.2.0-rc2:
    <http://svn.zoo-project.org/svn/tags/rel-1.2.0-rc2>
-   ZOO-Project Release 1.2.0-rc3:
    <http://svn.zoo-project.org/svn/tags/rel-1.2.0-rc3>

### ZOO-Project version 1.0.0 {#zoo_project_version_1.0.0}

#### Download {#download_1}

#### Archives {#archives_1}

[ZOO-Kernel-1.0.tar.bz2](http://www.zoo-project.org/dl/ZOO-Kernel-1.0.tar.bz2)
/ [ZOO-Kernel-1.0.zip](http://www.zoo-project.org/dl/ZOO-Kernel-1.0.zip)

## For developers {#for_developers}

    #sh
    svn checkout http://svn.zoo-project.org/svn/trunk zoo

For registred developers, you can use SSH or HTTPS protocol. Information
on how to setup your https account can be found
[here](http://zoo-project.org/trac/wiki/ZooDevDocumentation). For those
using SSH, as the server waiting incoming SSH connexions on the 1046
port, you\'ll have to edit your `~/.subversion/config` file to add a
tunnel. Let us name it as `zoossh`, you can then use the following
command :

    #sh
    # sed "s:\[tunnels\]:\[tunnels\]\nzoossh = /usr/bin/ssh -p 1046:g" -i ~/.subversion/config
    # svn co svn+zoossh://svn.zoo-project.org/var/svn/repos/trunk zoo-project

## ZOO Kernel MIT/X-11 License {#zoo_kernel_mitx_11_license}

Copyright © 2010-2011 GeoLabs

Permission is hereby granted, free of charge, to any person obtaining a
copy of this software and associated documentation files (the
\"Software\"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED \"AS IS\", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
