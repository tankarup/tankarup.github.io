# im@sparqlの使い方覚書
* アイマスの色んなデータをプログラムからゲットできるサービス[im@sparql](https://sparql.crssnky.xyz/imas/)の使い方をメモします。
* sparqlのことを全く知らず、そもそもデータベースのことも知らない状態から、使い方を模索した記録です。

## Webでまず試す
### 超基本
* [im@sparql](https://sparql.crssnky.xyz/imas/)のページにある'Input Query'に式を入力して"Submit"ボタンを押せば結果が表示される。
* 「?」がついているものは、いわゆる「変数」
* <>でくくられているものは、いわゆるキーワード
* 「I」「have」「a pen」、「My」「name is」「Ritsuko」のように3語で文をつくる。

### 基本式
* 「765ミリオンスターズ」の「メンバー」を変数「?member」に入れる。
* ?memberを出力する。

```sparql
SELECT ?member
WHERE {
     <https://sparql.crssnky.xyz/imasrdf/RDFs/detail/765MillionStars> <http://schema.org/member> ?member.
}
```

* 「765ミリオンスターズ」の「メンバー」を「?member」に入れ、
* 取得した「?member」の「体重」を変数「?weight」に入れる。
* ?member ?weightを出力する。

```sparql
SELECT ?member ?weight
WHERE {
     <https://sparql.crssnky.xyz/imasrdf/RDFs/detail/765MillionStars> <http://schema.org/member> ?member.
     ?member <http://schema.org/weight> ?weight.
}
```

* 「765ミリオンスターズ」の「メンバー」を「?member」に入れ、
* 取得した「?member」の「体重」を変数「?weight」に入れ、
* 続けて「?member」の「名前」を変数「?name」に入れ、
* 取得した「?name」は「日本語」だけに絞り込む。
* ?member ?weight ?nameを出力する。

```sparql
SELECT ?member ?weight ?name
WHERE {
     <https://sparql.crssnky.xyz/imasrdf/RDFs/detail/765MillionStars> <http://schema.org/member> ?member.
     ?member <http://schema.org/weight> ?weight;
        <http://schema.org/name> ?name.
    filter(LANG(?name) = 'ja')
}
```

### どんなキーワードが使えるのか
* 例えば [https://sparql.crssnky.xyz/imasrdf/RDFs/detail/Akizuki_Ritsuko](https://sparql.crssnky.xyz/imasrdf/RDFs/detail/Akizuki_Ritsuko) を開いてみると、『語彙』のところに「 http://schema.org/birthDate 」とか「 https://sparql.crssnky.xyz/imasrdf/URIs/imas-schema.ttl#Hobby 」とか記載されているのでこれを使う。
* 「Units」のタブに移動すると、『Unit Name』のところに「 https://sparql.crssnky.xyz/imasrdf/RDFs/detail/765ProAllstars 」とか記載されているのでこれを使う。

### 省略記法
いちいち`<https://~>`を入力するのは面倒なので、

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

あとは流れで。[公式ドキュメント](https://doc.crssnky.xyz/imasparql/)を読む。

## Javascriptに組み込む
TBD