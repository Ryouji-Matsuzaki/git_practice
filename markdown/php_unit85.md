## データ操作
### ファイルのアップロード

### ■ファイルアップロード

HTMLとPHPの連携により、利用者にファイルをアップロードしてもらう仕組みを用意する事ができます。

ファイルのアップロードを行うには、まずformタグに必要な属性を追加します。

** ファイルアップロードのための属性： **

* enctype="multipart/form-data"

* method="post"

methodは必ずpostになります。getでファイルデータを送る事はできません。

```html
<HTML>
    <head>
    </head>
    <body>
        <form enctype="multipart/form-data" action="sample.php" method="post">
            ファイル：<input name="userfile" type="file" />
            <input type="submit" value="送信">
        </form>
    </body>
</HTML>
```

ユーザーにファイルを選択させるため、入力部分を作成します。inputタグのtype属性にfileを指定すると、ファイル選択を行う仕組みが利用できます。

** inputをファイル選択項目にする方法： **

* type="file"

これでHTML側は準備完了です。ブラウザでファイルを選択し、送信ボタンを押すと、sample.phpに選択したファイルのデータが送信されます。

```html
<HTML>
    <head>
    </head>
    <body>
        <form enctype="multipart/form-data" action="sample.php" method="post">
            ファイル：<input name="userfile" type="file" />
            <input type="submit" value="送信">
        </form>
    </body>
</HTML>
```


### ■ファイルの受け取り

送信されたファイルのデータは、PHPで処理されます。そして、送信されたファイルデータは** $\_FILES**というスーパーグローバル変数に格納されます。

アップロードされたファイルを操作するには、この$\_FILESに格納された情報を利用します。

** $\_FILESからアップロードしたファイルを利用： **

* 変数 = $\_FILES[inputのname属性];


```php
<?php

// アップロードされたファイルの情報は
// $_FILESに多次元配列として格納されています
// var_dumpを利用して、内容を確認してみましょう
var_dump($_FILES['userfile']);

```


### ■ファイルの情報

$\_FILESには下記の情報が格納されています。

** $\_FILESに入っている情報： **

* 一時ファイルのパス（tmp_name）
* 正式なファイル名（name）
* ファイルのサイズ（size）
* エラー情報（error）

利用者からファイルがアップロードされると、ファイルにはランダムな名前が付けられ、一時フォルダで管理されます。tmp_nameは、その一時フォルダ上でのファイル名です。

```php
<?php

// アップロードファイルの取得情報を確認

// 正式ファイル名
echo $_FILES['userfile']['name'];
// 一時ファイル名
echo $_FILES['userfile']['tmp_name'];
// ファイルサイズ
echo $_FILES['userfile']['size'];
// エラー情報
echo $_FILES['userfile']['error'];
```

### ■ファイルをWebアプリの管理下へ

アップロードされたファイルは、一時フォルダに適当な名前で保管されています。これをそのままにすると、やがて削除されてしまいます。

そのため、該当ファイルを一時フォルダからWebアプリが管理しているフォルダへ移し、管理下に置きましょう。

** 一時ファイルの移動（move_uploaded_file）： **

```
変数 = move_uploaded_file(
　　　　一時フォルダのファイル名,
　　　　移動先のファイル名);
```

```php
<?php

// 一時フォルダのファイルをWebアプリの管理下に移動
// Webアプリのファイル管理は、filesフォルダで実施
$files_path = './files/' . $_FILES['userfile']['name'];
// ファイルを移動
if (move_uploaded_file($_FILES['userfile']['tmp_name'],
    $files_path)) {
    // 成功したら、中身を表示してみる
    echo file_get_contents($files_path);
}
```
