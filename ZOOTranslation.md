## ZOO Translation page {#zoo_translation_page}

You\'ll find here information about how the ZOO Kernel use the *gettext*
technology to translate on the fly both ZOO Kernel internal messages and
also ZOO Services Provider internal messages and zcfg content.

### Method to get your zcfg translated {#method_to_get_your_zcfg_translated}

First, use the following commands from your Services Provider directory
to extract all translatable messages from your ZCFG files :

    #!/bin/bash
    for j in cgi-env/*zcfg ; 
      do 
        for i in Title Abstract; 
         do
          grep $i $j | sed "s:$i = :_(\":g;s:$:\"):g" ;
         done;
     done > locale/.cache/my_service_string_to_translate.c

Now, produce the \'messages.po\' file based on the produced file and the
Services Provider source code using the following command :

    #!/bin/bash
    xgettext service.c locale/.cache/my_service_string_to_translate.c -o message.po -p locale/po/ -k_

Once you get the messages.po file, use the following command to create
the po file for the language you want to translate into, let suppose
that French language was chosen here :

    #!/bin/bash
    cd locale/po/
    msginit -i messages.po -o zoo_fr_FR.po -l fr

Obviously now you\'ll have to edit the zoo_fr_FR.po file with your
favorite text editor or using one of the following tools :

-   [poedit](http://www.poedit.net/)
-   [virtaal](http://translate.sourceforge.net/wiki/virtaal/index)
-   [transifex](https://www.transifex.net/projects/p/grass6/c/grass64/)

Once the zoo_fr_FR.po file exists, you can produce and install the
corresponding mo file using the following command :

    #!/bin/bash
    msgfmt locale/po/zoo_fr_FR.po -o /usr/share/locale/fr/LC_MESSAGES/zoo-services.mo

Now, to test if your Services Provider ZCFG and internal messages are
well translatable by the ZOO Kernel, please add the language argument to
you request, for instance : for the following url
<http://youserver/cgi-bin/zoo_loader.cgi?request=GetCapabilities&service=WPS>
use now this one
<http://youserver/cgi-bin/zoo_loader.cgi?request=GetCapabilities&service=WPS&language=fr-FR>

As many Services Provider Metadata File (zcfg) can be already
translated, it can be useful to use the following command to ensure
getting back all the translation for the specified language.

    #sh
    msgcat -o compilation.po $(find ../../ -name fr_FR.utf8.po)
    msgfmt compilation.po -o /usr/share/locale/fr/LC_MESSAGES/zoo-services.mo

