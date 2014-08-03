# .dwt Example 1

## 概要

DreamweaverのTempleteで`<!-- TemplateParam -->`と`<!-- TemplateBeginIf -->`を使って、ページ毎に`title`と`パンくずリスト`を生成するサンプル。

## 使い方

変数の設定

```
<!-- TemplateParam name="home" type="text" value="" -->
<!-- TemplateParam name="category" type="text" value="" -->
<!-- TemplateParam name="sub-category" type="text" value="" -->
```

例えば、タイトルに` | `セパレーターの有無を`<!-- TemplateBeginIf -->`で`<!-- TemplateParam -->`の値をチェックさせます。
条件を`!=''`として`TemplateParam`に値があれば` | `を付けて、値が無ければ何もしないので` | `は付かない。

```
<title>
@@(_document['sub-category'])@@
<!-- TemplateBeginIf cond="(_document['sub-category'])!=''" --> | <!-- TemplateEndIf -->
@@(_document['category'])@@
<!-- TemplateBeginIf cond="(_document['category'])!=''" --> | <!-- TemplateEndIf -->
@@(_document['home'])@@
</title>
```

同様にパンくずリストにも活用。

```
<nav class="bread">
  <ul>
    <li><a href="../index.html">@@(_document['home'])@@</a></li>
    <!-- TemplateBeginIf cond="(_document['category'])!=''" --><li> &gt; <a href="./index.html">@@(_document['category'])@@</a></li><!-- TemplateEndIf -->
    <!-- TemplateBeginIf cond="(_document['sub-category'])!=''" --><li> &gt; @@(_document['sub-category'])@@</li><!-- TemplateEndIf -->
  </ul>
</nav>
```
