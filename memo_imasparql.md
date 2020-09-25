# im@sparqlの使い方覚書
アイマスの色んなデータをプログラムでゲットできるサービスim@sparql( https://sparql.crssnky.xyz/imas/ )の使い方をメモします。

## Webでお試し
### 超基本
* 'Input Query'に式を入力して"Submit"ボタンを押せば結果が表示される。
* 「?」がついているものは、いわゆる「変数」

### 基本式
* 「765ミリオンスターズ」の「メンバー」を「?member」に入れる。
* ?memberを表示する。

```sparql
SELECT ?member
WHERE {
     <https://sparql.crssnky.xyz/imasrdf/RDFs/detail/765MillionStars> <http://schema.org/member> ?member.
}
```

* 「765ミリオンスターズ」の「メンバー」を「?member」に入れ、
* ゲットした「?member」の「体重」を「?weight」に入れる。
* ?member ?weightを表示する。

```sparql
SELECT ?member ?weight
WHERE {
     <https://sparql.crssnky.xyz/imasrdf/RDFs/detail/765MillionStars> <http://schema.org/member> ?member.
?member <http://schema.org/weight> ?weight.
}
```

* 「765ミリオンスターズ」の「メンバー」を「?member」に入れ、
* ゲットした「?member」の「体重」を「?weight」に入れ、
* 続けて「?member」の「名前」を「?name」に入れ、
* 「?name」は「日本語」だけに絞り込む。
* ?member ?weight ?nameを表示する。

```sparql
SELECT ?member ?weight ?name
WHERE {
     <https://sparql.crssnky.xyz/imasrdf/RDFs/detail/765MillionStars> <http://schema.org/member> ?member.
?member <http://schema.org/weight> ?weight;
<http://schema.org/name> ?name.
filter(LANG(?name) = 'ja')
}
```

### 使えるデータ
* 例えば https://sparql.crssnky.xyz/imasrdf/RDFs/detail/Akizuki_Ritsuko を開いてみると、『語彙』のところに「 http://schema.org/birthDate 」とか「 https://sparql.crssnky.xyz/imasrdf/URIs/imas-schema.ttl#Hobby 」とか記載されているのでこれを使う。
* 「Units」のタブに移動すると、『Unit Name』のところに「 https://sparql.crssnky.xyz/imasrdf/RDFs/detail/765ProAllstars 」とか記載されているのでこれを使う。

### 省略記法
いちいち\<https://~\>を入力するのは面倒なので、

```sparql
SELECT ?member
WHERE {
     <https://sparql.crssnky.xyz/imasrdf/RDFs/detail/765MillionStars> <http://schema.org/member> ?member.
}
```

↓

```sparql
PREFIX schema: <http://schema.org/>
PREFIX imasrdf: <https://sparql.crssnky.xyz/imasrdf/RDFs/detail/>

SELECT ?member
WHERE {
     imasrdf:765MillionStars schema:member ?member.
}
```

と省略する。


## Javascriptに組み込む
TBD