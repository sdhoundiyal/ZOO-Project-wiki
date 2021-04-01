## 演習

\_\_TOC\_\_ \[/ZOO-Project/ZOO-Project/wiki/ZooWorkshop/FOSS4GJapan/ja
ワークショップ 目次\]

以上で、zcfg メタデータファイルの記述方法と、
C言語またはPython言語の選択によって、`service.c` または
`ogr_service_provider.py` の短いコードが得られました。
この演習のゴールは、次のような複合ジオメトリサービスを実装することです :

-   Intersection
-   Union
-   Difference
-   SymDifference

### C バージョン {#c_バージョン}

`source.c`
ファイルの編集を選択された方は、このワークショップ演習を通して、追加した複合ジオメトリは、次のOGR
C-API 関数を使用しています:

-   [OGR_G\_Intersection](http://www.gdal.org/ogr/ogr__api_8h.html#5a271b5c7b72994120e7a6bbc7e7e5cb)(OGRGeometryH,
    OGRGeometryH)
-   [OGR_G\_Union](http://www.gdal.org/ogr/ogr__api_8h.html#f58f2cfbdb2497659d2eabea73d3b8a0)(OGRGeometryH,
    OGRGeometryH)
-   [OGR_G\_Difference](http://www.gdal.org/ogr/ogr__api_8h.html#497977bec6ecd9dade7a9694f776be64)(OGRGeometryH,
    OGRGeometryH)
-   [OGR_G\_SymmetricDifference](http://www.gdal.org/ogr/ogr__api_8h.html#d6dacf495617a230c6f19950bc415f17)(OGRGeometryH,
    OGRGeometryH)

`Boundary.zcfg ファイルを例に、 InputPolygon を InputEntity1 にして、同様に IntputEntity2 を追加することができます。ZOOメタデータファイルのそのほかの値についても、適当なメタデータ情報を設定してください。`

### Python バージョン {#python_バージョン}

`ogr_ws_service_provider.py`
ファイルの編集を選択された方は、このワークショップ演習を通して、追加した複合ジオメトリは、次の
`Geometry` インスタンスに適用された `osgeo.ogr` `Geometry`
関数を使用しています:

-   Intersection(Geometry)
-   Union(Geometry)
-   Difference(Geometry)
-   SymmetricDifference(Geometry)

`Boundary.zcfg ファイルを例に、 InputPolygon を InputEntity1 にして、同様に IntputEntity2 を追加することができます。ZOOメタデータファイルのそのほかの値についても、適当なメタデータ情報を設定してください。`

### サービスのテスト

ここで、複合ジオメトリサービスは、ローカル環境の上に配置されました。ブラウザ上から、前のセクションで作成した
`zoo-ogr.html`
をリロードしてください。そして新しいZOOサービスをテストしてください。\
\[/ZOO-Project/ZOO-Project/wiki/ZooWorkshop/FOSS4GJapan/ja
ワークショップ 目次\]
