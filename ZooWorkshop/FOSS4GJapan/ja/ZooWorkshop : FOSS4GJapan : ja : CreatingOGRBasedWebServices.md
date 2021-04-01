## OGRのWeb サービス作成 {#ogrのweb_サービス作成}

\_\_TOC\_\_
[/ZooWorkshop/FOSS4GJapan/ja/UsingZooFromOSGeoLiveVM前へ](ZooWorkshop : FOSS4GJapan : ja : UsingZooFromOSGeoLiveVM前へ "wikilink") \| [目次](ZooWorkshop : FOSS4GJapan : jaワークショップ "wikilink") \|
[///ZooWorkshop/FOSS4GJapan/ja/BuildingWPSClientUsingOL次へ](ZooWorkshop : FOSS4GJapan : ja : BuildingWPSClientUsingOL次へ "wikilink")

[Image(http://www.lafon-svv.com/html/images/ligne_horizontale.gif,width=530px,height=0.5px,nolink)](Image(http://www.lafon-svv.com/html/images/ligne_horizontale.gif,width=530px,height=0.5px,nolink) "wikilink")

### イントロダクション

このパートではZOOのサービス提供機能を作成します。これにはOSGeoLiveのDVDに含まれているZOOのインストーラーで組み込まれるOGRのC言語API、Pythonモジュールを使います。目標とするゴールは、OGRとGEOSベースの簡単な空間関数をWPSサービスとして使うことです。

最初にBoundary（境界）の関数からスタートしましょう。この関数の詳細については後ほど説明いたします。徐々にZOOサービスとしてコードを書き、テストを行います。
同じ手順でBuffer(バッファ領域の作成）、Centroid(重心）、Convex
Hull（凸構造体）の関数についても行います。一旦出来上がると、複数の幾何プロセス、たとえばIntersection（交差）,
Union（融合）, Difference（差異）、そして Symetric
Difference（対称性の差異）などがこのワークショップの終わりには組み込まれていることになります。

既に述べたように、このワークショップではサービスを記述する言語はCもしくはPython（もしくは両方！）を選ぶことができます。解説はC言語に沿って行いますが、この解説はPythonを利用する方にも非常に役立つ内容になっています。どちらの言語を使用するか決めたらインストラクターに報告してください。どちらの言語を選択されても、ワークショップの結果は同じです。

### ZOO メタデータファイルの準備 {#zoo_メタデータファイルの準備}

ZOOメタデータの用意

ZOOのサービスは、ZOOメタデータファイル(.zcfg)とZOOサービスプロバイダーと呼ばれる機能の応じたランタイム実装モジュールとの組み合わせによって成り立ちます。
まずはじめに順を追って.zcfgファイルを用意しましょう。
使う慣れているテキストエディタで
`/home/user/zoows/sources/zoo-services/ws_sp directory`フォルダにある
`Boundary.zcfg` を開いてください。
最初に、ファイル先頭にある括弧中に以下のようにサービス名を定義します。

    #sh
    [Boundary]

この名前は非常に重要です。この名前はサービス名になりサービスプロバイダーの機能を表します。タイトル（Title）とこのサービスが何を行うのかについての短い要約（Abstract）は、利用者のために書いておくべきです。

    #sh
    Title = Compute boundary.
    Abstract = Returns the boundary of the geometry on which the method is invoked.

これらのメタデータ情報は GetCapabilities リクエストによって返されます。

他にも `processVersion`　のような特定情報を追加することができます。
ZOOサービスが結果を保存する機能を持つかどうかを `storeSupported`
パラメータの値を `true`もしくは
`false`にすることで指定できます。また処理をバックグラウンドで行い、結果をステータスで通知するかどうかを
`statusSupported` の値で指定します。

    #sh
    processVersion = 1
    storeSupported = true
    statusSupported = true

ZOOサービス・メタデータファイルのメインのセクションでは、二つの重要事項を指定します。
In the main section of the ZOO Service metadata file, you must also
specify two important things:

-   `serviceProvider`　　サービスの関数を含むCの共用ライブラリの名前、またはPythonモジュール名
-   `serviceType`　　サービスに使用するプログラミング言語の指定 (値は C
    または Python となります。あなたが使用する言語とあわせてください。)

C !サービスプロバイダーの例 :

    #sh
    serviceProvider=ogr_ws_service_provider.zo
    serviceType=C

この例ではBoundary関数を含む `ogr_ws_service_provider.zo`
共用ライブラリを使うことになります。ライブラリファイルはZOOカーネルと同じディレクトリに置いてください。

Python !サービスプロバイダーの例 :

    #sh
    serviceProvider=ogr_ws_service_provider
    serviceType=Python

この例ではBoundary関数のPythonコードを含む `ogr_ws_service_provider.py`
ファイルを使うことになります。

メインセクションでは、下記の例のように他の任意の情報を追加することもできます。

    #sh
    <MetaData>
        Title = Demo
    </MetaData>

これで主要なメタデータ情報が定義できました。
次はZOOサービスで使われるデータの入力方法を定義します。サービスに必要な任意の入力を定義できます。
ZOOのカーネルは.zcfgファイルに定義したデータよりも多くのデータを処理するリクエストを受け付けることに注意してください。これらのデータはフィルタリングされることなくサービスへと渡されます。
この例のBoundaryサービスでは、一つのポリゴンが入力として使用され、それに対してBoundary関数が実行されます。

入力データ宣言は DataInputs ブロックで行われます。
書式はサービスを定義するときと同じで、名前は括弧でくくられています。同様にタイトルや要約を入力の
`MetaData` セクションに追加することができます。 `minOccurs` と
`maxOccurs`
のパラメータは必ず設定してください。これらは、どのパラメータがサービス関数で実行するのに必要なのかをZOOカーネルに通知するのに使われます。

    #sh
    [InputPolygon]
     Title = Polygon to compute boundary
     Abstract = URI to a set of GML that describes the polygon.
     minOccurs = 1
     maxOccurs = 1
     <MetaData lang="en">
         Test = My test
     </MetaData>

メタデータは、どのようなタイプのデータがサービスでサポートされるのかを定義します。このBoundary関数の例では、入力するポリゴンはGMLファイル形式またはJSON文字列形式で提供することができます。
次のステップではデフォルトのデータ形式とサポートする入力フォーマットを定義しましょう。それぞれのフォーマットはタイプに応じて
`LitteralData` または `ComplexData`
のブロックで定義する必要があります。ここでは最初の例として `ComplexData`
ブロックのみを使います。

    #sh
    <ComplexData>
     <Default>
       mimeType = text/xml
       encoding = UTF-8
     </Default>
     <Supported>
       mimeType = application/json
       encoding = UTF-8
     </Supported>
    </ComplexData>

次に、同様のメタデータ情報をサービスの出力についても定義します。`DataOutputs`　のブロック内に次のように定義します。

    #sh
    [Result]
     Title = The created geometry
     Abstract = The geometry containing the boundary of the geometry on which the method  was invoked.
     <MetaData lang="en">
       Title = Result
     </MetaData>
     <ComplexData>
      <Default>
       mimeType = application/json
       encoding = UTF-8
      </Default>
      <Supported>
       mimeType = text/xml
       encoding = UTF-8
      </Supported>
     </ComplexData>

この .zcfg ファイルのコピーは以下のURLからも入手できます :

<http://zoo-project.org/trac/browser/trunk/zoo-services/ogr/base-vect-ops/cgi-env/Boundary.zcfg>

ZOOメタデータファイルの修正が終わりましたら、ZOOのカーネルと同じディレクトリ
(この例では
`/usr/lib/cgi-bin`)へコピーしてください。これで以下のURLのリクエストが実行できるはずです：

<http://localhost/zoo/?Request=DescribeProcess&Service=WPS&Identifier=Boundary&version=1.0.0>

返って来る ProcessDescriptions XML
ドキュメントは、以下のようになっているはずです :

[Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/CreatingOGRBasedWebServices/Practical%20introduction%20to%20ZOO%20-%204.png,width=550px,nolink)](Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/CreatingOGRBasedWebServices/Practical%20introduction%20to%20ZOO%20-%204.png,width=550px,nolink) "wikilink")

GetCapabilities と
DescribeProcess　を実行には　.zfgファイルさえあれば完了します。簡単ですね？
このステップでは、ZOOカーネルに `Execute`をリクエストすれば、
以下のような `ExceptionReport` ドキュメントのレスポンスが返ってきます：

[Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/CreatingOGRBasedWebServices/Practical%20introduction%20to%20ZOO%20-%205.png,width=550px,nolink)](Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/CreatingOGRBasedWebServices/Practical%20introduction%20to%20ZOO%20-%205.png,width=550px,nolink) "wikilink")

もしPythonのサービスで実行すれば、同じようなエラーメッセージが返ってきます
:

[Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/CreatingOGRBasedWebServices/Practical%20introduction%20to%20ZOO%20-%206.png,width=550px,nolink)](Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/CreatingOGRBasedWebServices/Practical%20introduction%20to%20ZOO%20-%206.png,width=550px,nolink) "wikilink")

### ジオメトリサービスの実装

サービスプロバイダー作成と開発をステップバイステップで学習するため、はじめに
Boundary 関数専用の非常に簡単なものの作成に着目しましょう。 同様の手段を
Buffer、 Centroid と ConvexHull の実装に用います。

メタデータは既にOKです。それでは、サービスのコード作成に入りましょう。
ZOOサービスのコーディングの際注意すべき、もっとも重要なことは、あなたの作成する対応サービスは３つの引数（内部の
maps データ型または [Python
dictionaries](http://docs.python.org/tutorial/datastructures.html#dictionaries)）、整数型の実行ステータスを示す返り値(`SERVICE_FAILED`
or `SERVICE_SUCCEEDED`)を必要とするということです:

-   `conf` : 主な実行環境設定( main.cfg の記載に対応)
-   `inputs` : 入力に関する リクエスト / 初期値
-   `outputs` : 出力に関する リクエスト / 初期値

#### Boundary

#### C バージョン {#c_バージョン}

先に述べたとおり、ZOO カーネルは、
`maps`と呼ばれる特別なデータ型の中で、あなたの作成したサービス機能の引数を受け渡します。
サービスをC言語で記述するために、あなたはこのread/writeモードのデータ型にどのようにアクセスするかを学ぶ必要があります。
`maps` は、 `map` と呼ばれる `name` を格納するリストへのリンクで、
`content` `map` と次の `map` へのポインタ（またはそれ以上 `map`
がない場合は `NULL`
）からなります。ここに、あなたが確認可能な`zoo-kernel/service.h`
ファイル内で定義されたデータ型を示します:

    #c
    typedef struct maps{
        char* name;
        struct map* content;
        struct maps* next;
    } maps;

`maps` に含まれる `map`
も単純なリンクされたリストで、キー値のペアを格納するために用いられます。
したがって、`map` は `name` と `value` そして次の `map`
へのポインタからなります。
ここに、あなたが確認可能な`zoo-kernel/service.h`
ファイル内で定義されたデータ型を示します:

    #c
    typedef struct map{
        char* name;       /* The key */
        char* value;      /* The value */
        struct map* next; /* Next couple */
    } map;

部分的あるいは全部を埋めたデータ構造対が ZOO
カーネルからあなたのサービスへ受け渡されたとして、この意味は、各々の
`maps`
中の既存の`map`に関わる以外には、mapsの生成に関わらなくてよいという事です。
始めに知っておくべき関数は、 maps 内の map の詳細にアクセスするための
`getMapFromMaps` (`zoo-kernel/service.h` ファイルに定義) です。
この関数は次の３つの引数からなります:

-   `m` : 任意のmapを検索するのに用いる maps
    ポインタの代表値（※先頭ポインタ）
-   `name` : 検索するmapの名称を示す char\*
    の代表値（※文字列型の先頭ポインタ）
-   `key` : name という名称の map 内の固有キー

例えば、`inputs`という名の`maps` 内の `InputPolygon` の値の `map`
にアクセスする構文は次の通りです。Cコードではこのようになります:

    #c
    map* tmp=getMapFromMaps(inputs,"InputPolygon","value");

map
を得た時点で、次のような構文で値フィールドにアクセスすることが可能です:

    #c
    tmp->name
    tmp->value

maps `map`
のフィールドへのアクセスと読み込みはご存じのとおりです、今からこのようなデータ構造への書き込みはどのように行うかを学習しましょう。
これもまた `zoo-kernel/service.h` ファイルに定義された、単純な
`setMapInMaps` 関数を用います。 `setMapInMaps`
関数は４つの引数を必要とします:

-   `m` : 更新を行う `maps` ポンタ,
-   `ns` : 更新を行う `maps` の名称,
-   `n` : 値の更新を行う `map` の名称,
-   `v` : この map にセットする値.

これは、どのようにして`outputs`の`Result` `maps` 内のいくつかの `map`
の値を追加または編集するかという例です:

    #c
    setMapInMaps(outputs,"Result","value","Hello from the C World !");
    setMapInMaps(outputs,"Result","mimeType","text/plain");
    setMapInMaps(outputs,"Result","encoding","UTF-8");

既存の `map` の生成と更新には `setMapInMaps`
関数が使用されるということに注意してください。確かに、もし « value »
と呼ばれる `map`
が既存の場合（※NULLではないという意味）、その値は自動的に更新されます。
このワークショップでは、`maps` の `map` を使う場合、
`zoo-kernel/service.h` に定義された `addToMap` 関数を直接使用し、 `map`
内の値の追加と更新を行うこともできます：

-   `m` : a `map` pointer you want to update,
-   `n` : the name of the `map` you want to add or update the value,
-   `v` : the value you want to set in this `map`.

このデータ型はすべてのC言語ベースのZOOサービスにおいて使用されるほど、本当に重要です。そしてそれは、個々のデータ型の利用を除いて、他の言語でも同様にであることを示しています。たとえば
Python
の場合、ディクショナリー型が用いられ、さらに簡単に操作することができます。

ここに、Python言語による `maps` データ型の対応例があります（これは
`maps`の main 設定内の要約です）:

    #python
    main={
      "main": {
        "encoding": "utf-8",
        "version": "1.0.0",
        "serverAddress": "http://www.zoo-project.org/zoo/",
        "lang": "fr-FR,en-CA"
      },
      "identification": {"title": "The Zoo WPS Development Server",
        "abstract": "Development version of ZooWPS.",
        "fees": "None",
        "accessConstraints": "none",
        "keywords": "WPS,GIS,buffer"
      }
    }

maps と mapにどのように対応するかを知るために、OGR Boundary
関数を使用した最初の ZOO サービスを書く準備をしましょう。

すでにはじめにで述べたように、OSGeoLive に準備された MapServer WFS
server を使用します、それで完全なWFS
レスポンスを入力値に利用することが出来るでしょう。私たちは、完全なWFSレスポンスというよりはむしろ、ジオメトリオブジェクトだけを簡単に利用する
[OGR_G\_GetBoundary](http://www.gdal.org/ogr/ogr__api_8h.html#a797af4266c02846d52b9cf3207ef958)のように
OGR Geometry
関数を使用しましょう。まずはじめにすることは、完全なWFSレスポンスに定義されたジオメトリを抽出する関数を書くことです。私たちはそれを
createGeometryFromWFS と呼びましょう。

これはそのようなコードです:

    #c
    OGRGeometryH createGeometryFromWFS(maps* conf,char* inputStr){
      xmlInitParser();
      xmlDocPtr doc = xmlParseMemory(inputStr,strlen(inputStr));
      xmlChar *xmlbuff;
      int buffersize;
      xmlXPathContextPtr xpathCtx;
      xmlXPathObjectPtr xpathObj;
      char * xpathExpr="/*/*/*/*/*[local-name()='Polygon' or local-name()='MultiPolygon']";
      xpathCtx = xmlXPathNewContext(doc);
      xpathObj = xmlXPathEvalExpression(BAD_CAST xpathExpr,xpathCtx);
      if(xpathObj->nodesetval){
        errorException(conf, "Unable to parse Input Polygon","InvalidParameterValue");
        exit(0);
      }
      int size = (xpathObj->nodesetval) ? xpathObj->nodesetval->nodeNr : 0;
      xmlDocPtr ndoc = xmlNewDoc(BAD_CAST "1.0");
      for(int k=size-1;k>=0;k--){
        xmlDocSetRootElement(ndoc, xpathObj->nodesetval->nodeTab[k]);
      }
      xmlDocDumpFormatMemory(ndoc, &xmlbuff, &buffersize, 1);
      char *tmp=strdup(strstr((char*)xmlbuff,"?>")+2);
      xmlXPathFreeObject(xpathObj);
      xmlXPathFreeContext(xpathCtx);
      xmlFree(xmlbuff);
      xmlFreeDoc(doc);
      xmlCleanupParser();
      OGRGeometryH res=OGR_G_CreateFromGML(tmp);
      if(res==NULL){
        errorException(conf, "Unable to call OGR_G_CreatFromGML","NoApplicableCode");
        exit(0);
      }
      else
        return res;
    }

関数の本体に使用された errorException
の呼び出しに注目してください。この関数は `zoo-kernel/service_internal.h`
に定義されており、`zoo-kernel/service_internal.c`に記述されています。それは下記のように３つの引数を必要とします:

-   the main environment `maps`,
-   a `char*` representing the error message to display,
-   a `char*` representing the error code (as defined in the WPS
    specification -- Table 62).

言い換えると、WFSレスポンスがプロパティを解析されなかった場合、問題が起こったことをクライアントに知らせる
`ExceptionReport` 文が返されます。
WFSレスポンスからジオメトリオブジェクトを抽出する関数が書かれ、そしていまから
Boundary サービスの定義を始めることができます。これが Boundary
サービスの全体コードです:

    #c
    int Boundary(maps*& conf,maps*& inputs,maps*& outputs){
      OGRGeometryH geometry,res;
      map* tmp=getMapFromMaps(inputs,"InputPolygon","value");
      if(tmp==NULL){
        setMapInMaps(m,"lenv","message","Unable to parse InputPolygon");
        return SERVICE_FAILED;
      }
      map* tmp1=getMapFromMaps(inputs,"InputPolygon","mimeType");
      if(strncmp(tmp1->value,"application/json",16)==0)
        geometry=OGR_G_CreateGeometryFromJson(tmp->value);
      else
        geometry=createGeometryFromWFS(conf,tmp->value);
      if(geometry==NULL){
        setMapInMaps(m,"lenv","message","Unable to parse InputPolygon");
        return SERVICE_FAILED;
      }
      res=OGR_G_GetBoundary(geometry);
      tmp1=getMapFromMaps(outputs,"Result","mimeType");
      if(strncmp(tmp1->value,"application/json",16)==0){
        char *tmp=OGR_G_ExportToJson(res);
        setMapInMaps(outputs,"Result","value",tmp);
        setMapInMaps(outputs,"Result","mimeType","text/plain");
        free(tmp);
      }
      else{
        char *tmp=OGR_G_ExportToGML(res);
        setMapInMaps(outputs,"Result","value",tmp);
        free(tmp);
      }
      outputs->next=NULL;
      OGR_G_DestroyGeometry(geometry);
      OGR_G_DestroyGeometry(res);
      return SERVICE_SUCCEEDED;
    }

上記のコードに見られるように、私たちのサービスに受け渡されたデータインプットの
mimeType が初めにチェックされます:

    #c
      map* tmp1=getMapFromMaps(inputs,"InputPolygon","mimeType");
      if(strncmp(tmp1->value,"application/json",16)==0)
        geometry=OGR_G_CreateGeometryFromJson(tmp->value);
      else
        geometry=createGeometryFromWFS(conf,tmp->value);

基本的に、 `application/json` に設定された `mimeType`
を持つ入力を受け取った場合、ローカル関数の`OGR_G_CreateGeometryFromJson`
が、そうでない場合は `createGeometryFromWFS` を用います。
入力値はいつも同様の種類ではないことに注意してください。実際には、
`OGR_G_CreateGeometryFromJson`
を直接使用することは、JSON文字列は完全なGeoJSONのものではなくてジオメトリオブジェクトだけを含むものであることを意味します。とはいえ、あなたはこのコードをGeoJSON
文字列からジオメトリオブジェクトを抽出する関数を作り出すよう、簡単に完全なGeoJSON文字列を使えるように書き換えることができます（OGR
GeoJSON
Driverにも利用されているjson-cライブラリのインスタンスを使うことにより）。

入力されたジオメトリオブジェクトにアクセスできると、[OGR_G\_GetBoundary](http://www.gdal.org/ogr/ogr__api_8h.html#a797af4266c02846d52b9cf3207ef958)
関数を用いて、 res
のジオメトリオブジェクトに結果を格納することができます。その時、あなたはサポートされた出力フォーマットとして宣言した初期値の
GeoJSON または GML
として正しいフォーマットの値だけを格納しなければなりません。（※zcfgにそのように記載したので）
ZOO
カーネルは、事前にフィルされた出力値を提供し、たとえもしわれわれの例が、`application/json`
よりもむしろ `text/plain` を使用する mimeType
を使用して書き換えた場合は、あなたはキー名に対応する値を埋めることだけを行うように注意してください。実際には、クライアントからリクエストされたフォーマットにより（あるいは初期値のもの）、わたしたちは
JSON または GML 表現のジオメトリを準備ます。

    #c
      tmp1=getMapFromMaps(outputs,"Result","mimeType");
      if(strncmp(tmp1->value,"application/json",16)==0){
        char *tmp=OGR_G_ExportToJson(res);
        setMapInMaps(outputs,"Result","value",tmp);
        setMapInMaps(outputs,"Result","mimeType","text/plain");
        free(tmp);
      }
      else{
        char *tmp=OGR_G_ExportToGML(res);
        setMapInMaps(outputs,"Result","value",tmp);
        free(tmp);
      }

Boundary
ZOOサービスは実装されたので、あなたは共有ライブラリを作るためそれをコンパイルする必要があります。
service.hに定義された関数 (`getMapFromMaps`, `setMapInMaps` と
`addToMap`)を使用したので、あなたはそれらのファイルをあなたのCコードに含める必要があります。同様の必要性は
`zoo-kernel/service_internal.h`に宣言された errorException
関数にもあります。また、あなたのサービスオブジェクトファイルをランタイムの際の
`errorException` に使用される `zoo-kernel/service_internal.o`
をリンクする必要があります。そして、libxml2 と OGR C-API
にアクセスするために必要となるファイルもまた含めなければなりません。

シェアードライブラリに必要なものとして、
`extern "C"`を宣言するブロックコード内にあなたのコードを格納しなければなりません。サービスプロバイダディレクトリ(
`/home/zoows/sources/zoo-services/ws_sp`内の)ルートに置く service.c
ファイルの中に最終的なコードを格納されなければなりません。それはこのように見えます:

    #c
    #include "ogr_api.h"
    #include "service.h"
    extern "C" {
    #include <libxml/tree.h>
    #include <libxml/parser.h>
    #include <libxml/xpath.h>
    #include <libxml/xpathInternals.h>
    <YOUR SERVICE CODE AND OTHER UTILITIES FUNCTIONS>
    }

サービスの完全なソースは準備が出来たので、次にシェアードライブラリとしてコードをコンパイルした結果のシェアードオブジェクトに対応するサービスを生成する必要があります。これは次のコマンドを用いて行うことができます:

    #c
    g++ $CFLAGS -shared -fpic -o cgi-env/ServicesProvider.zo ./service.c $LDFLAGS

`CFLAGS` and `LDFLAGS`
環境変数は事前にセットする必要があることに注意してください。

`CFLAGS`
はインクルードされたヘッダを探すために求められるパスおよび`ogr_api.h`,
libxml2 directory, `service.h` と `service_internal.h`
ファイルのディレクトリへのパスのすべてを含む必要があります。OSGeoLive
環境のおかげで、いくつかの添付されたツールを用いてそのような値を取り出すことができます:`xml2-config`
と `gdal-config` どちらも `--cflags`
条件に用いられます。それらは要求通りのパスを生成します。

もし `zoo-services` 内のメインディレクトリに ZOO
サービスのプロバイダーを作成する説明を続けるならば、あなたのカレントパス(`/home/user/zoows/sources/zoo-services/ws_sp`)に対して相対的な
`../../zoo-kernel`ディレクトリにある ZOO
カーネルとソースツリーを見ることができます。あなたのソースツリーを別の場所に移動させる場合でも全く同様のコマンドラインを使ったコードコンパイルを保持するために相対パスなのですが、ZOO
カーネルのフルパスを使用することもできることに注意してください。コンパイラーが
`service.h` と `service_internal.h`
を見つけることが出来るようにするために `CFLAGS` に
`-I../../zoo-kernel`を加える必要があります。

完全な `CFLAGS` 記述はこの通りです:

    #sh
    CFLAGS=<tt>gdal-config --cflags</tt> <tt>xml2-config --clfags</tt> -I../../zoo-kernel/

`CFLAGS`
に正しくセットするインクルードパスをたので、リンクに対応するライブラリ(`LDFLAGS`環境変数として定義)に取り組みましょう。gdal
と libxml2 ライブラリに対するリンクの場合、 上記と同じツールに
`--cflags` のかわりに `--libs` を用いることができます。完全な`LDFLAGS`
の記述はこの通りです:

    #sh
    LDFLAGS=<tt>gdal-config --libs</tt> <tt>xml2-config --libs</tt> ../../zoo-kernel/service_internal.o

次にコードのコンパイル時に手助けをする Makefile を作成します。ZOO
サービスプロバイダディレクトリのルートに短い Makefile
を書きましょう、下記の行を含みます:

    #sh
    ZOO_SRC_ROOT=../../zoo-kernel/
    CFLAGS=-I${ZOO_SRC_ROOT} <tt>xml2-config --cflags</tt> <tt>gdal-config --cflags</tt>
    LDFLAGS=<tt>xml2-config --libs</tt> <tt>gdal-config --libs</tt>${ZOO_SRC_ROOT}/service_internal.o

    cgi-env/ogr_ws_service_provider.zo: service.c
        g++ ${CFLAGS} -shared -fpic -o cgi-env/ogr_ws_service_provider.zo ./service.c $ {LDFLAGS}
    clean:
        rm -f cgi-env/ogr_ws_service_provider.zo

この `Makefile` を使用して、ZOO サービスプロバイダディレクトリから make
を実行すると、 `cgi-env` に結果として `ogr_ws_service_provider.zo`
というファイルが得られます。

メタデータファイルと ZOO サービスシェアードオブジェクトの両方が
`cgi-env` ディレクトリにできました。新しい ServicesProvider
を配置するために、ZOO カーネルがあるディレクトリ `/usr/lib/cgi-bin` に
ZOOサービスシェアードオブジェクトと対応するメタファイルの両方をコピーしましょう。このタスクを実行するためには
`sudo` コマンドを用いなければなりません:

    #sh
    sudo cp ./cgi-env/* /usr/lib/cgi-bin

これで、ZOO
サービスのソースツリーの意味するところが解りましたね。`cgi-env`
ディレクトリはあなたの新しいサービスまたはサービスプロバイダを、`cgi-env`
のコンテンツを `cgi-bin` ディレクトリにコピーするという簡単な方法で
配置をするためのものです。

make install と直接タイプすることで、新しいサービスプロバイダを
ZOOカーネルで利用可能にするために、 `Makefile`
に下記の行を追加することが出来ることに注意してください:

    #sh
    install:
        sudo cp ./cgi-env/* /usr/lib/cgi-bin

これで、 ZOO
サービスプロバイダは、ZOOカーネルを通しての実行リクエストから利用される準備が出来ました。

#### Python バージョン {#python_バージョン}

ZOO のサービスするプロバイダの実装に Python を使用するため、cgi-env
ディレクトリにある ogr_ws_service_provider.py
のすべてのコピーするコードは下記のとおりです。実際、Pythonのようなインタプリタ言語では、極めて簡単な配置ステップで作られるサービスの配置以外にはなにもコンパイルする必要がありません:

    #python
    import osgeo.ogr
    import libxml2

    def createGeometryFromWFS(my_wfs_response):
        doc=libxml2.parseMemory(my_wfs_response,len(my_wfs_response))
        ctxt = doc.xpathNewContext()
        res=ctxt.xpathEval("/*/*/*/*/*[local-name()='Polygon' or local- name()='MultiPolygon']")
        for node in res:
            geometry_as_string=node.serialize()
            geometry=osgeo.ogr.CreateGeometryFromGML(geometry_as_string)
            return geometry
        return geometry

    def Boundary(conf,inputs,outputs):
        if inputs["InputPolygon"]["mimeType"]=="application/json":
            geometry=osgeo.ogr.CreateGeometryFromJson(inputs["InputPolygon"]["value"])
        else:
            geometry=createGeometryFromWFS(inputs["InputPolygon"]["value"])
        rgeom=geometry.GetBoundary()
        if outputs["Result"]["mimeType"]=="application/json":
            outputs["Result"]["value"]=rgeom.ExportToJson()
            outputs["Result"]["mimeType"]="text/plain"
        else:
            outputs["Result"]["value"]=rgeom.ExportToGML()
        geometry.Destroy()
        rgeom.Destroy()
        return 3

私たちは既に詳細を伝えていて、コードは同様な方法で作られているため、ここでは関数本体については述べません。

実行の前にすることは、`cgi-env` のファイルを `cgi-bin`
にコピーすることだけです:

    #sh
    sudo cp ./cgi-env/* /usr/lib/cgi-bin

インストールセクションに対応した簡単な `Makefile` 次のように書かれます:

    #sh
    install:
        sudo cp ./cgi-env/* /usr/lib/cgi-bin/

最後に、簡単にZOO サービスプロバイダのメインディレクトリから make
install を実行すると、ZOO プロバイダーが配置されます。

#### Execute リクエストを使用したテスト {#execute_リクエストを使用したテスト}

##### 単純かつ読みづらい方法

皆さんは、ご自分の ogr_ws_service_provider
と呼ばれる、ZOOカーネルツリーに配置された ZOO
サービスプロバイダとして格納された OGR Boundary
サービスのコピーがあり、サービスをテストするために Execute
リクエストを次の通りに使うことができます:

[link](http://localhost/cgi-bin/zoo_loader.cgi?request=Execute&service=WPS&version=1.0.0&Identifier=Boundary&DataInputs=InputPolygon=Reference@xlink:href=http%3A%2F%2Flocalhost%2Fcgi-bin%2Fmapserv%3Fmap%3D%2Fvar%2Fwww%2Fwfs.map%26SERVICE%3DWFS%26REQUEST%3DGetFeature%26VERSION%3D1.0.0%26typename%3Dregions%26SRS%3DEPSG%3A4326%26FeatureID%3Dregions.3192)

    http://localhost/cgi-bin/zoo_loader.cgi?request=Execute&service=WPS&version=1.0.0&Identifier=Boundary&DataInputs=InputPolygon=Reference@xlink:href=http%3A%2F%2Flocalhost%2Fcgi-bin%2Fmapserv%3Fmap%3D%2Fvar%2Fwww%2Fwfs.map%26SERVICE%3DWFS%26REQUEST%3DGetFeature%26VERSION%3D1.0.0%26typename%3Dregions%26SRS%3DEPSG%3A4326%26FeatureID%3Dregions.3192

上記のURLに見られるように、 `DataInputs` KVP 値内の `xlink:href`
キーにある、OSGeoLive上の MapServer WFSサーバーや、
`Reference`にセットされる `InputPolygon` の値を URLエンコードされた WFS
リクエストとして使用します。エンコードされていない
WFSリクエストに対応したものは次の通りです:

<http://localhost/cgi-bin/mapserv?map=/var/www/wfs.map&SERVICE=WFS&REQUEST=GetFeature&VERSION=1.0.0&typename=regions&SRS=EPSG:4326&featureid=regions.3192>

サービスの実行に利用される入力値についての情報を得たい場合、lineage=true
を付け加えることができることに注意してください。さらに、後で再利用するために
ZOO サービスの `ExecuteResponse`
ドキュメントを格納する必要があるかもしれません。このような場合、前のリクエストに
`storeExecuteResponse=true` を追加してください。このパラメータ指定を
true
にしていない実行の時と比べて、ZOOカーネルの挙動は正確には同じでないということに注意してください。実際、このようなリクエストでは、ZOO
カーネルは statusLocation の属性に対する `ExecuteResponse`
を返し、それは実行中の結果あるいは最後に `ExecuteResponse`
に置かれた情報をクライアントに与えます。

リクエスト中で `storeExecuteResponse` が true に設定された場合、
`ExecuteResponse` がどのようになるかの例は次の通りです:

[Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/CreatingOGRBasedWebServices/Practical%20introduction%20to%20ZOO%20-%207.png,width=550px)](Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/CreatingOGRBasedWebServices/Practical%20introduction%20to%20ZOO%20-%207.png,width=550px) "wikilink")

statusLocation にしたがって、以前にリクエストした時に得られたものと同じ
`ExecuteResponse`
が得られました。クライアントアプリケーションのキャッシングシステムを備えているということで大変便利になるということに注意してください。

以前のリクエストのすべての `ResponseForm`
を指定しておらず、リクエストされなかったなら、作成した zcfg
ファイルに定義された初期値で用いられる `application/json` `mimeType`
に基づく `ResponseDocument` が返されます。しかしながら、クエリーの
`ResponseDocument` パラメータに `mimeType=text/xml`
属性を加えることで、ZOO
カーネルにどのような種類の結果が欲しいかを伝えることができます。以前のリクエストに対して、このパラメータを追加することで
GML 表記の結果を得られます:

[link](http://localhost/cgi-bin/zoo_loader.cgi?request=Execute&service=WPS&version=1.0.0&Identifier=Boundary&DataInputs=InputPolygon=Reference@xlink:href=http%3A%2F%2Flocalhost%2Fcgi-bin%2Fmapserv%3Fmap%3D%2Fvar%2Fwww%2Fwfs.map%26SERVICE%3DWFS%26REQUEST%3DGetFeature%26VERSION%3D1.0.0%26typename%3Dregions%26SRS%3DEPSG%3A4326%26FeatureID%3Dregions.3192&ResponseDocument=Result@mimeType=text/xml)

    http://localhost/cgi-bin/zoo_loader.cgi?request=Execute&service=WPS&version=1.0.0&Identifier=Boundary&DataInputs=InputPolygon=Reference@xlink:href=http%3A%2F%2Flocalhost%2Fcgi-bin%2Fmapserv%3Fmap%3D%2Fvar%2Fwww%2Fwfs.map%26SERVICE%3DWFS%26REQUEST%3DGetFeature%26VERSION%3D1.0.0%26typename%3Dregions%26SRS%3DEPSG%3A4326%26FeatureID%3Dregions.3192&ResponseDocument=Result@mimeType=text/xml

WPS仕様による定義では、完全な `ResponseDocument` ではなくデータだけの
`RawDataOutput`を問い合わせることができます。そうするためには、次に示されるリクエストのように、リクエストの
`ResponseDocument` を `RawDataOutput` に置き換えるだけです。:

[link](http://localhost/cgi-bin/zoo_loader.cgi?request=Execute&service=WPS&version=1.0.0&Identifier=Boundary&DataInputs=InputPolygon=Reference@xlink:href=http%3A%2F%2Flocalhost%2Fcgi-bin%2Fmapserv%3Fmap%3D%2Fvar%2Fwww%2Fwfs.map%26SERVICE%3DWFS%26REQUEST%3DGetFeature%26VERSION%3D1.0.0%26typename%3Dregions%26SRS%3DEPSG%3A4326%26FeatureID%3Dregions.3192&RawDataOutput=Result@mimeType=application/json)

    http://localhost/cgi-bin/zoo_loader.cgi?request=Execute&service=WPS&version=1.0.0&Identifier=Boundary&DataInputs=InputPolygon=Reference@xlink:href=http%3A%2F%2Flocalhost%2Fcgi-bin%2Fmapserv%3Fmap%3D%2Fvar%2Fwww%2Fwfs.map%26SERVICE%3DWFS%26REQUEST%3DGetFeature%26VERSION%3D1.0.0%26typename%3Dregions%26SRS%3DEPSG%3A4326%26FeatureID%3Dregions.3192&RawDataOutput=Result@mimeType=application/json

最後に、このワークショップの次のセクションにあるクライアントアプリケーションの開発に使用するために、にこの種のリクエストをJSON文字列形式で取得するよう
`mimeType`
の初期値を戻しておくことに注意してください。（※次のセクションでは
mimeType=application/json を使用します）

##### リクエストの単純化と可読性

このワークショップのはじめから用いられた例をみると、複雑で長いURLを作成して
GET に用いられるExecute リクエストを書くことは時により困難です。
次のリクエスト例では、そういうことですので、POST XML
リクエストを用いましょう。初めに、以前の Execute
で使用したリクエストに対応する XML は次のとおりです:

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 ../wpsExecute_request.xsd">
     <ows:Identifier>Boundary</ows:Identifier>
     <wps:DataInputs>
      <wps:Input>
       <ows:Identifier>InputPolygon</ows:Identifier>
       <ows:Title>Playground area</ows:Title>
       <wps:Reference xlink:href="http://localhost/cgi-bin/mapserv?map=/var/www/wfs.map&amp;SERVICE=WFS&amp;REQUEST=GetFeature&amp;VERSION=1.0.0&amp;typename=regions&amp;SRS=EPSG:4326&amp;featureid=regions.3192"/>
      </wps:Input>
     </wps:DataInputs>
     <wps:ResponseForm>
      <wps:ResponseDocument>
       <wps:Output>
        <ows:Identifier>Result</ows:Identifier>
        <ows:Title>Area serviced by playground.</ows:Title>
        <ows:Abstract>Area within which most users of this playground will live.</ows:Abstract>
       </wps:Output>
      </wps:ResponseDocument>
     </wps:ResponseForm>
    </wps:Execute>

XML リクエストを簡単に実行するために、test_services.html と呼ばれる HTML
フォームを `/var/www`
に準備しました。次に示すリンクを使用してそれにアクセスすることができます:
<http://localhost/test_services.html>.

ブラウザでこのページを開いてください、テキストエリアフィールド内に簡単に
XML リクエストを埋めて、« run using XML Request »
送信ボタンをクリックします。サービスが GET
リクエストを使用して実行したときと同様に結果を得られます。スクリーンショットは、上記に示されたリクエストを含む
HTML フォームとページの下部にある iframe に表示された
`ExecuteResponse`を示します:

[Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/CreatingOGRBasedWebServices/Practical%20introduction%20to%20ZOO%20-%208.png,width=550px)](Image(http://www.zoo-project.org/trac/raw-attachment/wiki/ZooWorkshop/FOSS4GJapan/CreatingOGRBasedWebServices/Practical%20introduction%20to%20ZOO%20-%208.png,width=550px) "wikilink")

`xlink:href`
の値はこのようなデータ入力を取り扱うもっとも簡単な方法です。もちろん、ジオメトリの完全なJSON文字列を使う事もでき、それは次に示す
XML リクエスト例のとおりです:

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 ../wpsExecute_request.xsda">
     <ows:Identifier>Boundary</ows:Identifier>
     <wps:DataInputs>
      <wps:Input>
       <ows:Identifier>InputPolygon</ows:Identifier>
       <wps:Data>
        <wps:ComplexData mimeType="application/json">
    { "type": "MultiPolygon", "coordinates": [ [ [ [ -105.998360, 31.393818 ], [ -106.212753, 31.478128 ], [ -106.383041, 31.733763 ], [ -106.538971, 31.786198 ], [ -106.614441, 31.817728 ], [ -105.769730, 31.170780 ], [ -105.998360, 31.393818 ] ] ], [ [ [ -94.913429, 29.257572 ], [ -94.767380, 29.342451 ], [ -94.748405, 29.319490 ], [ -95.105415, 29.096958 ], [ -94.913429, 29.257572 ] ] ] ] }
        </wps:ComplexData>
       </wps:Data>
      </wps:Input>
     </wps:DataInputs>
     <wps:ResponseForm>
      <wps:ResponseDocument>
       <wps:Output>
        <ows:Identifier>Result</ows:Identifier>
        <ows:Title>Area serviced by playground.</ows:Title>
        <ows:Abstract>Area within which most users of this playground will live.</ows:Abstract>
       </wps:Output>
      </wps:ResponseDocument>
     </wps:ResponseForm>
    </wps:Execute>

もし、すべてがうまくいったなら、引数として JSONジオメトリの Boundary
が受け渡され、サービスは GML と JSON
の両方を入力データとして取り扱えるということです。先のリクエストで、私たちは、`ComplexData`ノードの属性に追加した`mimeType`に、
入力データが `text/xml` `mimeType` ではなくて `application/json`
文字列を指定して受け渡される指定をしました。それは、以前に述べたように
`@mimeType=application/json` を追加したのと同じことです。

#### その他の関数サービスの作成 (ConvexHull and Centroid) {#その他の関数サービスの作成_convexhull_and_centroid}

Boudary
の単純なサービスコードがありますので、全く同じ数の引数:ジオメトリをもつ
ConvexHull と Centroid を簡単に追加することができます。実装の詳細と
ConvexHull サービスの配置については、下記に示すたとおりです。 Centroid
についても同様です。

#### C バージョン {#c_バージョン_1}

まず次に示すコードを `service.c` ソースコードに追加しましょう:

    #c
    int ConvexHull(maps*& conf,maps*& inputs,maps*& outputs){
      OGRGeometryH geometry,res;
      map* tmp=getMapFromMaps(inputs,"InputPolygon","value");
      if(tmp==NULL){
        setMapInMaps(conf,"lenv","message","Unable to fetch InputPolygon value.");
        return SERVICE_FAILED;
      }
      map* tmp1=getMapFromMaps(inputs,"InputPolygon","mimeType");
      if(strncmp(tmp1->value,"application/json",16)==0)
        geometry=OGR_G_CreateGeometryFromJson(tmp->value);
      else
        geometry=createGeometryFromWFS(conf,tmp->value);
      if(geometry==NULL){
        setMapInMaps(conf,"lenv","message","Unable to parse InputPolygon value.");
        return SERVICE_FAILED;
      }
      res=OGR_G_ConvexHull(geometry);
      tmp1=getMapFromMaps(outputs,"Result","mimeType");
      if(strncmp(tmp1->value,"application/json",16)==0){
        char* tmp=OGR_G_ExportToJson(res);
        setMapInMaps(outputs,"Result","value",tmp);
        setMapInMaps(outputs,"Result","mimeType","text/plain");
        free(tmp);
      }
      else{
        char* tmp=OGR_G_ExportToGML(res);
        setMapInMaps(outputs,"Result","value",tmp);
        free(tmp);
      }
      OGR_G_DestroyGeometry(geometry);
      OGR_G_DestroyGeometry(res);
      return SERVICE_SUCCEEDED;
    }

この新しいコードは、Boundary
サービスと全く同じです。ただ一つ我々が変更するのは、[OGR_G\_ConvexHull](http://www.gdal.org/ogr/ogr__api_8h.html#7a93026cfae8ee6ce25546dba1b2df7d)
関数が呼ばれている行の部分です (前に使用した
`OGR_G_GetBoundary`ではなく)。関数をまったくコピーペーストすることは良くありませんので、すべての場合において、新しいサービスの関数本体の記述を行うもっと一般的な方法があります。次に示す常用関数は単純化のためのものです:

    #c
    int applyOne(maps*& conf,maps*& inputs,maps*& outputs,OGRGeometryH (*myFunc) (OGRGeometryH)){
      OGRGeometryH geometry,res;
      map* tmp=getMapFromMaps(inputs,"InputPolygon","value");
      if(tmp==NULL){
        setMapInMaps(conf,"lenv","message","Unable to fetch InputPolygon value.");
        return SERVICE_FAILED;
      }
      map* tmp1=getMapFromMaps(inputs,"InputPolygon","mimeType");
      if(strncmp(tmp1->value,"application/json",16)==0)
        geometry=OGR_G_CreateGeometryFromJson(tmp->value);
      else
        geometry=createGeometryFromWFS(conf,tmp->value);
      if(geometry==NULL){
        setMapInMaps(conf,"lenv","message","Unable to parse InputPolygon value.");
        return SERVICE_FAILED;
      }
      res=(*myFunc)(geometry);
      tmp1=getMapFromMaps(outputs,"Result","mimeType");
      if(strncmp(tmp1->value,"application/json",16)==0){
        char *tmp=OGR_G_ExportToJson(res);
        setMapInMaps(outputs,"Result","value",tmp);
        setMapInMaps(outputs,"Result","mimeType","text/plain");
        free(tmp);
      }
      else{
        char *tmp=OGR_G_ExportToGML(res);
        setMapInMaps(outputs,"Result","value",tmp);
        free(tmp);
      }
      outputs->next=NULL;
      OGR_G_DestroyGeometry(geometry);
      OGR_G_DestroyGeometry(res);
      return SERVICE_SUCCEEDED;
    }

次に、完全な関数名の代わりに `myFunc`
と呼ばれる関数ポインタを使用します。Boundary
サービスをこの方法で再実装する方法は次のとおりです:

    #c
    int Boundary(maps*& conf,maps*& inputs,maps*& outputs){
      return applyOne(conf,inputs,outputs,&OGR_G_GetBoundary);
    }

`service.c` 内に定義された、この `applyOne` ローカル関数を用いて,
その他のサービスを次のように定義できます:

    #c
    int ConvexHull(maps*& conf,maps*& inputs,maps*& outputs){
      return applyOne(conf,inputs,outputs,&OGR_G_ConvexHull);
    }
    int Centroid(maps*& conf,maps*& inputs,maps*& outputs){
      return applyOne(conf,inputs,outputs,&MY_OGR_G_Centroid);
    }

`applyOne` 関数の一般化により２つの新しいサービス : ConvexHull and
Centroidが ZOO プロバイダに追加されます。

Centroid
の前に、[OGR_G\_Centroid](http://www.gdal.org/ogr/ogr__api_8h.html#23f5a19a81628af7f9cc59a37378cb2b)にあるように、返されるジオメトリオブジェクト以外にも既存のポリゴンをセットするジオメトリを入力値とする
`MY_OGR_Centroid` 関数を定義する必要があります。マルチポリゴンの
ConvexHull を確保するためでもあります。コードは次のとおりです:

    #c
    OGRGeometryH MY_OGR_G_Centroid(OGRGeometryH hTarget){
      OGRGeometryH res;
      res=OGR_G_CreateGeometryFromJson("{\"type\": \"Point\", \"coordinates\": [0,0] }");
      OGRwkbGeometryType gtype=OGR_G_GetGeometryType(hTarget);
      if(gtype!=wkbPolygon){
        hTarget=OGR_G_ConvexHull(hTarget);
      }
      OGR_G_Centroid(hTarget,res);
      return res;
    }

サービスを配置するため、 cgi-env ディレクトリから `ConvexHull.zcfg` と
`Centroid.zcfg` として、 `Boundary.zcfg` をコピーします。
次に、前にも行ったとおりの手順で、 `Execute`
リクエストの実行とテストのために、最初の行のサービス名を書き換える必要があります。Idenitifier
の値を、実行するサービスのリクエストに対応するように、 ConvexHull または
Centroid に書き換えます。

ここでは、 `GetCapabilities` と `DescribeProcess`
リクエストはメタデータを書き換えなかったので、中途半端な（Boundaryの）情報を返すこと、.zcfg
に修正した値をセットできることに注意してください。ところで、テストの目的で使用されるので、入力と出力の名前と、default/supported
フォーマットも同じものが使われています。

#### Python バージョン {#python_バージョン_1}

    #python
    def ConvexHull(conf,inputs,outputs):
        if inputs["InputPolygon"]["mimeType"]=="application/json":
            geometry=osgeo.ogr.CreateGeometryFromJson(inputs["InputPolygon"]["value"])
        else:
            geometry=createGeometryFromWFS(inputs["InputPolygon"]["value"])
        rgeom=geometry.ConvexHull()
        if outputs["Result"]["mimeType"]=="application/json":
            outputs["Result"]["value"]=rgeom.ExportToJson()
            outputs["Result"]["mimeType"]="text/plain"
        else:
            outputs["Result"]["value"]=rgeom.ExportToGML()
        geometry.Destroy()
        rgeom.Destroy()
        return 3

再度、Boundary
の関数を簡単にコピーペーストして、Geometry関数が呼ばれている行を変更します。やはり、C言語で行ったように、もっと一般化して単純にする方法を教えましょう。

まずはじめに、各々のサービス関数で同様に用いられる InputPolygon
ジオメトリの抽出にある最初のステップですが、まずはじめにその関数を作りましょう。
同様に出力値を埋め、他の関数に対しても自動的に行われるよう定義しましょう。２つの関数
(extractInputs and outputResult) はつぎのとおりです:

    #python
    def extractInputs(obj):
        if obj["mimeType"]=="application/json":
            return osgeo.ogr.CreateGeometryFromJson(obj["value"])
        else:
            return createGeometryFromWFS(obj["value"])
        return null

    def outputResult(obj,geom):
        if obj["mimeType"]=="application/json":
            obj["value"]=geom.ExportToJson()
            obj["mimeType"]="text/plain"
        else:
            obj["value"]=geom.ExportToGML()

Boundary
関数のコードを、下記に示す関数定義により、最小にすることができます:

    #python
    def Boundary(conf,inputs,outputs):
        geometry=extractInputs(inputs["InputPolygon"])
        rgeom=geometry.GetBoundary()
        outputResult(outputs["Result"],rgeom)
        geometry.Destroy()
        rgeom.Destroy()
        return 3

次に、ConvexHull and Centroid
サービスの定義については下記コードになります:

    #python
    def ConvexHull(conf,inputs,outputs):
        geometry=extractInputs(inputs["InputPolygon"])
        rgeom=geometry.ConvexHull()
        outputResult(outputs["Result"],rgeom)
        geometry.Destroy()
        rgeom.Destroy()
        return 3

    def Centroid(conf,inputs,outputs):
        geometry=extractInputs(inputs["InputPolygon"])
        if geometry.GetGeometryType()!=3:
            geometry=geometry.ConvexHull()
        rgeom=geometry.Centroid()
        outputResult(outputs["Result"],rgeom)
        geometry.Destroy()
        rgeom.Destroy()
        return 3

Pythonにおいても。マルチポリゴンを取り扱う ConvexHull
を使う必要があるということに注意してください。

Cバージョンで説明したように、Boundary.zcfg を `ConvexHull.zcfg` と
`Centroid.zcfg` の各々にコピーしてください。 そして、make install
コマンドを使い、サービスプロバイダを再配置します。

#### バッファサービス作成

我々はバッファサービスを使用することができますが、他のサービスに比べ多くの引数を必要とします。実際コードは、境界や凸包、そして中心点生成サービスを実装する際に使用されるものと少々異なっているからです。

バッファサービスもまた、入力引数としてジオメトリを必要としますが、使用するのは
`BufferDistance` のパラメータです。これにより、単純な整数値として
`BufferDistance` の`LitteralData`
ブロックを定義できるでしょう。そのような種類の入力値の読込処理は、以前使用したのと同じ機能が使用されます。

#### C バージョン {#c_バージョン_2}

あなたが、最初の境界サービスのソースコードへ戻るならば、以下について非常に複雑になったとは気づかれないでしょう。実際、あなたはBufferDistance
引数のアクセスに加えて、[OGR_G\_Buffer](http://www.gdal.org/ogr/ogr__api_8h.html#1ca0bd5c0fcb4b1af3c3973e467b0ec0)
が（ `OGR_G_GetBoundary`
の代わりに）呼び出されるべように変更するだけです。ここに、全てのlcodeを示します：

    int Buffer(maps*& conf,maps*& inputs,maps*& outputs){
      OGRGeometryH geometry,res;
      map* tmp1=getMapFromMaps(inputs,"InputPolygon","value");
      if(tmp==NULL){
        setMapInMaps(conf,"lenv","message","Unable to fetch InputPolygon value.");
        return SERVICE_FAILED;
      }
      map* tmp1=getMapFromMaps(inputs,"InputPolygon","mimeType");
      if(strncmp(tmp->value,"application/json",16)==0)
        geometry=OGR_G_CreateGeometryFromJson(tmp->value);
      else
        geometry=createGeometryFromWFS(conf,tmp->value);
      double bufferDistance=1;
      tmp=getMapFromMaps(inputs,"BufferDistance","value");
      if(tmp!=NULL)
        bufferDistance=atof(tmp->value);
      res=OGR_G_Buffer(geometry,bufferDistance,30);
      tmp1=getMapFromMaps(outputs,"Result","mimeType");
      if(strncmp(tmp1->value,"application/json",16)==0){
        char *tmp=OGR_G_ExportToJson(res);
        setMapInMaps(outputs,"Result","value",tmp);
        setMapInMaps(outputs,"Result","mimeType","text/plain");
        free(tmp);    
      }
      else{
        char *tmp=OGR_G_ExportToGML(res);
        setMapInMaps(outputs,"Result","value",tmp);
        free(tmp);    
      }
      outputs->next=NULL;
      OGR_G_DestroyGeometry(geometry);
      OGR_G_DestroyGeometry(res);
      return SERVICE_SUCCEEDED;
    }

新しいコードは、あなたの`service.c` ファイルに挿入し、再コンパイルの後に
`/usr/lib/cgi-bin/`
ディレクトリにあるZOOサービスプロバイダーの旧バージョンと置き換えなければなりません。もちろん、対応するZOOのメタデータファイルを同じディレクトリに置かなければなりません。

以前の説明にあったように、ZOOカーネルは、zcfg
ファイルで定義されるよりも多くの引数を渡すことができます。ですから、`Boundary.zcfg`
ファイルを `Buffer.zcfg`
と改名したコピーを使用して、バッファ識別子を記載してみましょう。その際、以前も行ったように
`Execute`
リクエストを用いてサービスをテストしてください。そうすると、`ResponseDocument`
でバッファの結果を得られるでしょう。

`BufferDistance`
入力値がサービスをパスするかどうか上のコードをチェックすることに注意しましょう。
もし、そうでなければデフォルト値として1を使用するようにして下さい。前の入力値を使わないようにするためです。

リクエストに DataInputs
値を加えることによって、ジオメトリのバッファを計算するのにあなたのサービスで使用された`BufferDistance`
値を変更することができます。KVP シンタックスを使用することで、各
DataInputs が、セミコロンによって分割されることに注意してください。

以前のリクエスト：

    DataInputs=InputPolygon=Reference@xlink:href=http%3A%2F%2Flocalhost%2Fcgi-bin%2Fmapserv%3FSERVICE%3DWFS%26REQUEST%3DGetFeature%26VERSION%3D1.0.0%26typename%3Dregions%26SRS%3DEPSG%3A4326%26FeatureID%3Dregions.3192

以下のように置き換えます：

    DataInputs=InputPolygon=Reference@xlink:href=http%3A%2F%2Flocalhost%2Fcgi-bin%2Fmapserv%3FSERVICE%3DWFS%26REQUEST%3DGetFeature%26VERSION%3D1.0.0%26typename%3Dregions%26SRS%3DEPSG%3A4326%26FeatureID%3Dregions.3192;BufferDistance=2

`BufferDistance` 値を 2
に設定する場合、異なる結果が与えられるでしょう。なぜなら、ソースコード上で1をデフォルト値と定めたため、いかなるパラメータも渡されないからです。

ここで、 <http://localhost/test_services.html>
のHTMLフォームから使用するXML形式における同じクエリを見つけられるでしょう：

    #xml
    <wps:Execute service="WPS" version="1.0.0" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 ../wpsExecute_request.xsda">
     <ows:Identifier>Buffer</ows:Identifier>
     <wps:DataInputs>
      <wps:Input>
       <ows:Identifier>InputPolygon</ows:Identifier>
       <ows:Title>Playground area</ows:Title>
       <wps:Reference xlink:href="http://localhost/cgi-bin/mapserv?map=/var/www/wfs.map&amp;SERVICE=WFS&amp;REQUEST=GetFeature&amp;VERSION=1.0.0&amp;typename=regions&amp;SRS=EPSG:4326&amp;featureid=regions.3192"/>
      </wps:Input>
      <wps:Input>
       <ows:Identifier>BufferDistance</ows:Identifier>
       <wps:Data>
        <wps:LiteralData uom="degree">2</wps:LiteralData>
       </wps:Data>
      </wps:Input>
     </wps:DataInputs>
     <wps:ResponseForm>
      <wps:ResponseDocument>
       <wps:Output>
        <ows:Identifier>Buffer</ows:Identifier>
        <ows:Title>Area serviced by playground.</ows:Title>
        <ows:Abstract>Area within which most users of this playground will live.</ows:Abstract>
       </wps:Output>
      </wps:ResponseDocument>
     </wps:ResponseForm>
    </wps:Execute>

#### Python バージョン {#python_バージョン_2}

　すでにユーティリティ機能の createGeometryFromWFS と outputResult
を定義しているので、コードはこれと同じくらい簡単です：

    #python
    def Buffer(conf,inputs,outputs):
        geometry=extractInputs(inputs["InputPolygon"])
        try:
            bdist=int(inputs["BufferDistance"]["value"])
        except:
            bdist=10
        rgeom=geometry.Buffer(bdist)
        outputResult(outputs["Result"],rgeom)
        geometry.Destroy()
        rgeom.Destroy()
        return 3

ここでは、!\[\"BufferDistance\"]!\[\"value\"]
のインプットを、ジオメトリインスタンスにおけるバッファ方法を引数として加えたのみです。一旦このコードを、ogr_ws_service_provider.py
ファイルに追加した後で、ZOOカーネルのディレクトリの中に（もしくは、ZOOサービスプロバイダのルートディレクトリからインストールする形で）それをコピーしてください。また、次のセクションで
Buffer.zcfg ファイルを詳述する必要があることに注意してください。

#### バッファ メタファイル {#バッファ_メタファイル}

クライアントにサービスがこのパラメータをサポートすることを知らせるようにするため､
サービス･メタデータ･ファイルに `BufferDistance`
を加えなければなりません｡ そうした上で､あなたのオリジナルのBoundary.zcfg
ファイルを Buffer.zcfg ファイルとしてコピーして､DataInputs
のブロックに以下のラインを加えてください｡

    [BufferDistance]
    Title = Buffer Distance
    Abstract = Distance to be used to calculate buffer.
    minOccurs = 0
    maxOccurs = 1
    <LiteralData>
    DataType = float
    <Default>
    uom = degree
    value = 10
    </Default>
    <Supported>
    uom = meter
    </Supported>
    </LiteralData>

`minOccurs は､パラメータの入力が任意であることを意味するために 0 が設定されているので､パスを通す必要はありません｡ むしろ､ZOOカーネルは､任意のパラメータのためにデフォルト設定値とサービス機能にデフォルト値を通すことを知る必要があります｡`

あなたは､ここで `Buffer.zcfg` ファイルのフルコピーを取得できます｡

<http://zoo-project.org/trac/browser/trunk/zoo-services/ogr/base-vect-ops/cgi-env/Buffer.zcfg>

あなたは､バッファサービスついて GetCapabilities や DescribeProcess
そして Execute をZOOカーネルにたずねることができます｡

[////ZooWorkshop/FOSS4GJapan/ja/UsingZooFromOSGeoLiveVM前へ](ZooWorkshop : FOSS4GJapan : ja : UsingZooFromOSGeoLiveVM前へ "wikilink") \| [目次](ZooWorkshop : FOSS4GJapan : jaワークショップ "wikilink") \|
[//////ZooWorkshop/FOSS4GJapan/ja/BuildingWPSClientUsingOL次へ](ZooWorkshop : FOSS4GJapan : ja : BuildingWPSClientUsingOL次へ "wikilink")

