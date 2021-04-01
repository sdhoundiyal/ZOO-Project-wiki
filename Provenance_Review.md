## ZOO-Project Provenance review {#zoo_project_provenance_review}

ZOO-Project code providence review, covering issues raised for each part
of ZOO-Project. The goal here is to check the headers (fill them in if
needed) and confirm that the information is correct.

### Source code review {#source_code_review}

ZOO-Project global licensing informations can be found in the
[LICENSE](http://www.zoo-project.org/trac/browser/trunk/zoo-project/LICENSE)
file.

#### Thirds

  Part                  Status   message   Link
  --------------------- -------- --------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  thirds/cgic           **c**              [license.txt](http://www.zoo-project.org/trac/browser/trunk/thirds/cgic206/license.txt)
  thirds/dirent-win32   **c**              [dirent.h](http://www.zoo-project.org/trac/browser/trunk/thirds/dirent-win32/dirent.h#L31) / [dirent.c](http://www.zoo-project.org/trac/browser/trunk/thirds/dirent-win32/dirent.c#L132)
  thirds/unistd         **c**              [unistd.h](http://www.zoo-project.org/trac/browser/trunk/thirds/include/unistd.h#L1)

#### ZOO-Kernel {#zoo_kernel}

  Part         Status   message   Link
  ------------ -------- --------- -----------------------------------------------------------------------------------------
  ZOO-Kernel   **c**              [LICENSE](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-kernel/LICENSE)

#### ZOO-API {#zoo_api}

  Part                       Status   message   Link
  -------------------------- -------- --------- ----------------------------------------------------------------------------------------------------------
  ZOO-API.js - ZOO-API       **c**              [ZOO-api.js](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-api/js/ZOO-api.js#L1)
  ZOO-proj4js.js - ZOO-API   **c**              [ZOO-proj4js.js](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-api/js/ZOO-proj4js.js#L1)

#### ZOO-Services {#zoo_services}

  Part                             Status   message   Link
  -------------------------------- -------- --------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  cgal                             **c**              [service.c](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/cgal/service.c#L1)
  gdal (dem,grid,translate,warp)   **c**              [dem](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/gdal/dem/service.c#L1) / [grid](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/gdal/grid/service.c#L1) / [translate](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/gdal/translate/service.c#L1) / [warp](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/gdal/warp/service.c#L1)
  gdal (profile)                   **c**              [profile](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/gdal/profile/service.c#L1)
  gdal (ndvi)                      **c**              [ndvi.py](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/gdal/ndvi/cgi-env/ndvi.py#L1)
  ogr (base-vect-ops)              **c**              [service.c](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/ogr/base-vect-ops/service.c#L1)
  ogr (base-vect-ops-py)           **c**              [ogr_sp.py](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/ogr/base-vect-ops-py/cgi-env/ogr_sp.py#L1)
  ogr (ogr2ogr)                    **c**              [ogr2ogr](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/ogr/ogr2ogr/service.c#L1)
  qrencode                         **c**              [qrencode](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/qrencode/qrenc-service.c#L3)
  utils                            **c**              [status](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/utils/status/service.c#L1)
  hello-fortran                    **c**              [LICENSE](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/hello-fortran/LICENSE#L1)
  hello-java                       **c**              [HelloJava.java](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/hello-java/HelloJava.java#L1)
  hello-js                         **c**              [helo.js](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/hello-js/cgi-env/hello.js#L1)
  hello-perl                       **c**              [Hello.pl](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/hello-perl/Hello.pl#L1)
  hello-php                        **c**              [helo.php](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/hello-php/hello.php#L3)
  hello-py                         **c**              [test_service.py](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/hello-py/cgi-env/test_service.py#L1)
  openoffice                       **c**              [oo_service.py](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/openoffice/cgi-env/oo_service.py#L1) / [Exporter.py](http://www.zoo-project.org/trac/browser/trunk/zoo-project/zoo-services/openoffice/cgi-env/Exporter.py#L1)

### Status definitions {#status_definitions}

` n::`\
`   not checked yet`\
` p::`\
`   check in progress`\
` s::`\
`   check is stuck, header or license requires developer attention`\
` c::`\
`   checked, all clear`\
` w::`\
`   checked, warning (missing information)`\
` x::`\
`   checked, fix me! requires developer attention `

