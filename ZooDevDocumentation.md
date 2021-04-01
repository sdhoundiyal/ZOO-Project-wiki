## ZOO-Project Developper documentation {#zoo_project_developper_documentation}

You\'ll find here informations about the access granted to you when you
are a developper.

First you get an SSH account which give you access to the
ZOO-Project.org server through the 1046 port. To connect use the
following:

    ssh -p 1046 <DEV_USER>@zoo-project.org 

Using this account you can access the ZOO-Project SVN server using SSH,
configuring a specific tunnel in your local `.subversion/config` file.

You can configure your https access to the SVN server using the
following commands on the ZOO-Project.org server:

    htpasswd /var/svn/repos/conf/svnusers <DEV_USER>

You can now access the SVN server using https protocol using your
`<DEV_USER>`{=html}.

