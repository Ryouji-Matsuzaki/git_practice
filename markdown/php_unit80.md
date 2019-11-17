## データ操作
### 入力内容の取得

### ■入力内容の取得

一般的なWebページでは、ただ情報を表示するだけでなく、利用者に様々な情報を入力してもらっています。

しかし、Webページに入力項目を作っただけでは、入力された情報を利用することはできません。PHPで受け取るために、入力部分に設定を行う必要があります。

ここでは、利用者の入力情報をPHPで扱うために必要な

* HTMLの記述
* PHPの処理

を学習します。

### ■HTMLの記述

PHPで利用者の入力内容を利用するには、HTML上で下記の作業が必要となります。

** HTML上で実施する事： **

* 入力項目へ名前を付ける(name属性の利用)
* 入力項目をformタグで括る
* formタグのaction先を指定する
* submitボタンを作成する

入力項目へ名前を付けるには、inputやselect、textareaなどに用意されているname属性を利用します。PHPではこのname属性に設定された名前で、利用者の入力値を利用する事になります。


```html
<html>
  <head>
    <title>コントロールサンプル</title>
  </head>
  <body>
    <form action="./sample.php" method="post">
      <input type="text" name="txtName">
      <input type="checkbox" name="chkTest">
      <input type="radio" name="rdoSample">
      <input type="button" name="btnTest">
      <input type="submit" name="btnSubmit">

      <select name="cmbList"></select>
      <textarea name="mulText"></textarea>
    </form>
  </body>
</html>

```

PHPへ入力内容を送るには、formタグを利用します。formタグで括った中にある入力項目の情報がformタグのaction属性に指定されたURL(パス)へ転送されます。

右記の例では、action属性に「./sample.php」と記述されています。この場合、利用者が送信ボタン（submit）を押すと、inputやselectの利用者の入力情報は、sample.phpというPHPファイルへ送信される事になります。


```html
<html>
  <head>
    <title>コントロールサンプル</title>
  </head>
  <body>
    <form action="./sample.php" method="post">
      <!-- formタグで括られた入力項目はこれら -->
      <input type="text" name="txtName">
      <input type="checkbox" name="chkTest">
      <input type="radio" name="rdoSample">
      <input type="button" name="btnTest">
      <input type="submit" name="btnSubmit">

      <select name="cmbList"></select>
      <textarea name="mulText"></textarea>
    </form>
  </body>
</html>

```

### ■PHPの処理

HTMLからsubmitにより送信された情報は、サーバーで受け取り、PHPファイル上で利用するために、** $\_GET ** もしくは ** $\_POST ** というスーパーグローバル変数に連想配列の形でセットされます。

変数にはローカル変数・グローバル変数と、定義される場所によって変数を使用できる範囲が異なりましたが、スーパーグローバル変数は、スクリプト全体を通してすべての範囲(スコープ)で使用可能な変数のことです。

スーパーグローバル変数には次のようなものがあります。

* $GLOBALS  
* $\_SERVER
* **$\_GET**
* **$\_POST**
* $\_FILES
* $\_COOKIE
* $\_SESSION
* $\_REQUEST
* $\_ENV

これらは全て覚える必要はありません。今回はよく使われる **$\_GET**、**$\_POST** について詳しく見ていきます。

$\_GETと$\_POST、どちらにデータが格納されるかは、formタグのmethod属性により決定します。
formタグのmethod属性がgetであれば、$\_GETに。postであれば、$\_POSTに格納されます。

** $\_GETの利用方法（$\_POSTも同様）： **

* 変数 = $\_GET[HTMLのname属性値];

```php
<?php
// sample.phpで送信されたデータを利用する方法

// テキストボックスの情報
echo $_POST['txtName'];
// チェックボックスの情報
echo $_POST['chkTest'];
// ラジオボタンの情報
echo $_POST['rdoSample'];
// ボタンの情報
echo $_POST['btnTest'];
// コンボボックス（select）の情報
echo $_POST['cmbList'];
// テキストエリアの情報
echo $_POST['mulText'];
```
