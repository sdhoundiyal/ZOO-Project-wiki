## OSGeoLiveの仮想マシンによる ZOO の利用 {#osgeoliveの仮想マシンによる_zoo_の利用}

\_\_TOC\_\_
[/ZooWorkshop/FOSS4GJapan/ja/Introduction/前へ](ZooWorkshop : FOSS4GJapan : ja : Introduction : 前へ "wikilink") \| [目次](ZooWorkshop : FOSS4GJapan : jaワークショップ "wikilink") \|
[///ZooWorkshop/FOSS4GJapan/ja/CreatingOGRBasedWebServices次へ](ZooWorkshop : FOSS4GJapan : ja : CreatingOGRBasedWebServices次へ "wikilink")

[OSGeoLive](http://live.osgeo.org/) は
[Xubuntu](http://www.xubuntu.org/)
を基にしたライブDVDの一つであり、インストールをすることなく、多くのオープンソース地理空間情報に関連するソフトウェアを利用することができる。これは全てフリーオープンソースソフトウェアから構成され、今年からテストを目的としてZOO1.0も含んでいます。

### ZOOカーネルのインストール

導入部分での説明の通り、すぐにZOOカーネルを利用できるように、OSGeoLive仮想マシンイメージディスクが、あなたのコンピュータにインストールされています。仮想マシンイメージディスクの使用は、ZOOカーネルの使用や、ローカル環境でのZOOサービス開発のための最も簡単な方法であり、Cサービスのコンパイルや、Pythonの動作をするための必要な設定はすべて行われています。ZOOに関連するすべての教材やソースコードは、
`/home/user/zoows`
ディレクトリに置かれています。ワークショップ中は、このディレクトリ内で作業します。　ZOOカーネルのバイナリバージョンもまた、
`/home/user/zoows/sources/zoo-kernel`
にコンパイルされ保存されているので、ZOOカーネルを使用するためには、`/usr/lib/cgi-bin`
ディレクトリの`zoo_loader.cgi`と `main.cfg`
の２つの重要なファイルをコピーするだけです。以下のコマンドに従ってください。:

    #sh
    sudo cp ~/zoows/sources/zoo-kernel/zoo_loader.cgi /usr/lib/cgi-bin
    sudo cp ~/zoows/sources/zoo-kernel/main.cfg /usr/lib/cgi-bin

このワークショップ中は、ZOOカーネルと `zoo_loader.cgi`
スクリプトについては、同じものとして扱いますので注意してください。

`main.cfg`
ファイルは、`identification`や`provider`に関するメタ情報だけでなく、いくつかの重要な設定情報も含まれています。ファイルは様々なセクション、主に`main`,
`identification`と`provider`をデフォルトとして構成されています。もちろん特定のサービスのために、新しいセクションの追加は自由に行ってください。
しかし、`env`
及び`lenv`セクションの名前は、特定の方法で扱われることに注意してください。
`env`
は、実行中のあなたのサービスに必要とする環境変数を定義します。例えば、あなたのサービスがフレームバッファ上のXサーバーへのアクセスを要求したとき、この特異性を考慮するためにDISPLAY=:1の１行をenvセクション中に追加することができます。`env`セクションと同様に、`main.cfg`には`lenv`
セクションがあります。これは、ZOOカーネルやZOOサービスによって、実行中のサービスのステータス情報が記述されます。例えば、あなたのサービスがうまく動作しなかった際、クライアントに返答される`ExecuteResponse`
の`Status`ノード中に表示されるように、`lenv`の中の`message`の値を設定することができます。
また、もしあなたのサービスが実行に時間がかり、処理ステータスの情報が取得できる場合、完了した実行中のサービスタスクをパーセンテージを表示するために
、`lenv`に値を0から100の間で設定できます。

このファイルを確認してください。３つの重要なパラメーターが下記に示されています。

-   `serverAddress` : ZOOカーネルへ接続するためのURL
-   `tmpPath` : 一時ファイル保存場所へのフルパス
-   `tmpUrl` :
    serverAddressに関連した一時ディレクトリへアクセスするためのURLフルパス

実行中の仮想マシンから使用される`main.cfg`ファイルの値は次の通りです：

    #sh
    serverAddress=http://localhost/zoo
    tmpPath=/var/www/temp
    tmpUrl=../temp/

気がついているかもしれませんが、`tmpUrl`は`serverAddress`からの相対URLであり、ディレクトリでなければなりません。ZOOカーネルが`zoo_loader.cgi`スクリプトの完全URLとして使用できるとしても、ZOOカーネルの完全な機能や読み易さのため、http://localhost/zoo/
として直接URLを使用できるように、Apacheの標準設定を変更しなければなりません。

最初に、zooディレクトリを`/var/www/`（ApacheのDocumentRootディレクトリ）の中に作成してください。次に
`/etc/apache2/sites-available/default`の設定ファイルを編集し、`/var/www`に関する`Directory`ブロックの後に、下記の数行を追加してください:

    #sh
    <Directory /var/www/zoo/>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        allow from all
    </Directory>

`/var/www/zoo` のなかに、 `.htaccess`
を新しく作り、下記の数行を記述してください:

    #sh
    RewriteEngine on
    RewriteRule call/(.*)/(.*) /cgi-bin/zoo_loader.cgi?request=Execute&service=WPS&version=1.0.0&Identifier=$1&DataInputs=sid=$2&RawDataOutput=Result [L,QSA]
    RewriteRule (.*)/(.*) /cgi-bin/zoo_loader.cgi?metapath=$1 [L,QSA]
    RewriteRule (.*) /cgi-bin/zoo_loader.cgi [L,QSA]

この最後のファイルをApacheで実行するためには、以下のようにロードファイルをコピーして、Apache
モジュールの書き換えを実行しなければなりません。:

    #sh
    sudo cp /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/

または、`a2enmod` ツールを次のように使用してください:

    #sh
    a2enmod rewrite

Apacheウェブサーバーを再起動することで、ZOOカーネルにアクセスできます。:

    #sh 
    sudo /etc/init.d/apache2 restart

このワークショップではOSGeoLive環境から、その他の２つのソフトウェアを使用します。

まず MapServer
は、これから設定していくZOOサービスのためのWFS入力データとして使用します。[////ZooWorkshop/FOSS4GJapan/ja/CreatingOGRBasedWebServicesセクション３](ZooWorkshop : FOSS4GJapan : ja : CreatingOGRBasedWebServicesセクション３ "wikilink") では、オークニー社（日本のポリゴンデータ）から提供された
MapServer データセットを、作成したサービスで使用されます。

OpenLayers ライブラリもまた、OSGeo Live
仮想マシンイメージディスクの中で利用できます。[/////ZooWorkshop/FOSS4GJapan/BuildingWPSClientUsingOL\#BuildingaWPSclientusingOpenLayersセクション４](ZooWorkshop : FOSS4GJapan : BuildingWPSClientUsingOL\#BuildingaWPSclientusingOpenLayersセクション４ "wikilink") で、新しく作られた ZOO サービスの問合せに使う簡単な WPS
クライアントアプリケーションに利用されます。

GDALライブラリのPythonモジュールとOGR
C-APIを使用するため、対応するヘッダーファイル、ライブラリ、関連ファイルを必要とします。すべてがデフォルトで、OSGeoLiveパッケージ上で使用できる状態になっています。

### GetCapabilities で ZOO のインストレーションをテストする {#getcapabilities_で_zoo_のインストレーションをテストする}

ブラウザからの以下のリクエストに従って簡単にZOOカーネルのクエリーを実行できます:

<http://localhost/cgi-bin/zoo_loader.cgi?Request=GetCapabilities&Service=WPS>

これで、以下の有効な `Capabilities` XMLドキュメントを得ることができます:

[Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/UsingZooFromOSGeoLiveVM/Practical%20introduction%20to%20ZOO%20-%202.png,width=550px,align=center,nolink)](Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/UsingZooFromOSGeoLiveVM/Practical%20introduction%20to%20ZOO%20-%202.png,width=550px,align=center,nolink) "wikilink")

利用可能なZOOサービスがないと、`ProcessOfferings`
セクションで、`no Process`
ノードが戻ってくることに注意してください。以下のコマンドをつかってコマンドラインからの
`GetCapabilities` リクエストも行うことができます:

    #sh
    cd /usr/lib/cgi-bin
    ./zoo_loader.cgi “request=GetCapabilities&service=WPS”

次のスクリーンショットに表示されているように、ブラウザと同様の結果が返されます:

[Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/UsingZooFromOSGeoLiveVM/Practical%20introduction%20to%20ZOO%20-%203.png,width=400px,align=center,nolink)](Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/UsingZooFromOSGeoLiveVM/Practical%20introduction%20to%20ZOO%20-%203.png,width=400px,align=center,nolink) "wikilink")

コマンドラインからのZOOカーネルの実行は、新しいサービスの開発に便利です。

### ZOO Services Providerディレクトリの準備 {#zoo_services_providerディレクトリの準備}

まず作業を簡略化するために、新しいServices
Providerを作成する際に使用されるディレクトリ構造について説明します:

-   メインServices Providerディレクトリはこれらを含みます:
    -   すべての `zcfg` メタファイルと 共有オブジェクト（C Shared
        Library あるいは Python もモジュール）サービスを含む `cgi-env`
        ディレクトリ
    -   Services Providerをコンパイルするためには `Makefile` と `*c`
        ファイルが必要です。

上記のことに注意しながら、ws_sp メイン Services Provider
ディレクトリを、`/home/user/zoows/sources/`にある既存の
zoo-servicesディレクトリに作成してください。

    #sh
    mkdir -p /home/user/zoows/sources/zoo-services/ws_sp/cgi-env

次のセクションで `Makefile` とC 、Python Service Shared
Objectのコードについて説明していきます。

\
[//////ZooWorkshop/FOSS4GJapan/ja/Introduction/前へ.](ZooWorkshop : FOSS4GJapan : ja : Introduction : 前へ. "wikilink") \| [目次](ZooWorkshop : FOSS4GJapan : jaワークショップ "wikilink") \|
[////////ZooWorkshop/FOSS4GJapan/ja/CreatingOGRBasedWebServices次へ](ZooWorkshop : FOSS4GJapan : ja : CreatingOGRBasedWebServices次へ "wikilink")

