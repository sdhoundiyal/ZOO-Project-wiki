## Download ZOO source code {#download_zoo_source_code}

### SVN Repository {#svn_repository}

To download the lastest repository of this project use the following
command :

    #sh
    svn checkout http://svn.zoo-project.org/svn/trunk zoo

If you have a ZOO Developer account you can use the following command :

    #sh
    sed "s:\[tunnels\]:\[tunnels\]\nzoo-ssh = /usr/bin/ssh -p 1046:g" -i ~/.subversion/config
    svn checkout svn+zoo-ssh://svn.zoo-project.org/var/svn/repos/trunk zoo

