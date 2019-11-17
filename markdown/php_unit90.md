## DB操作
### PDOによるDB操作

### ■PDOによるDB操作の流れ

PDOによるDB操作の大まかな流れは、下記になります。

**PDOによるDB操作の流れ：**

1. PDOオブジェクト作成（DB接続）

2. SQL文作成（パラメータを含むSQL文の作成）

3. PDOオブジェクトにSQL文を設定

4. SQL文のパラメータを置換（bindValue）

5. SQL文の実行

6. （SELECTの場合）実行結果を取得

7. PDOオブジェクトの破棄（DB切断）

下記のUserテーブルを使って、説明します。

|ID|Name|Age|
|:----|:----|:----|
|1|添田亮司|34|
|2|林星河|29|

### ■PDOオブジェクト作成

PDOを利用して、まずはデータベースに接続します。

**PDOによる接続：**
```
　　変数 = new PDO(
　　　　接続文字, ユーザ―名, パスワード);
```

ここで利用する接続文字は、

* データベースの種類、
* ホスト、
* データベース名、
* 利用文字コード

などを連結したものです。各情報を「;」で区切って渡します。


```php
<?php
// 接続文字列作成
// データベースは、MySQL
// ホストは、localhost
// データベース名は、Challenge_db
// 利用文字コードは、utf8
// ID/パスワードは、hayashi/mypassword
$dns =  'mysql:host=localhost;';
$dns .= 'dbname=Challenge_db;';
$dns .= 'charset=utf8';

// データベースへ接続
$pdo_obj = new PDO($dns, 'hayashi', 'mypassword');
```

接続文字、ユーザー名、パスワードに間違いが無ければPDOのオブジェクトが生成されます。

間違っている場合、エラーが発生します。

また、データベースとの接続を切断する場合は、オブジェクトを入れた変数をnullで上書きします。

**データベースの切断：**
* PDOオブジェクトが入った変数 = null;

```php
<?php

// データベースへ接続
$pdo_obj = new PDO($dns, 'hayashi', 'mypassword');

// データベースの切断
$pdo_obj = null;
```


### ■SQL文作成（パラメータを含むSQL文の作成）

データベースを操作するには、PHPからデータベースへSQL文を送る必要があります。

まずは、SQL文を作ります。SQL文はPHP上で文字列として作成します。

この際、SQL文を実行する際に実際の値と置き換える部分にパラメータを埋め込みます。

**後で置き換えるパラメータ：**
* 「:name」⇒「SEIGA」に置き換えるパラメータ
* 「:age」⇒「29」に置き換えるパラメータ

```php
<?php
// UserテーブルのAgeが29のレコードの
// Nameを「SEIGA」に変更するSQL

// パラメータを含むSQL文を作成する。
// 「:name」には後で「SEIGA」を
// 「:age」には後で29を
// 当てはめるため、パラメータを埋め込む
$sql = "UPDATE User ";
$sql .= "SET Name = :name WHERE Age = :age";

```

### ■PDOオブジェクトにSQL文を設定

作成したパラメータを含むSQL文は、PDOオブジェクトのprepare関数に渡します。

すると、PDOオブジェクトは渡されたSQL文を含むプリペアードステートメントを生成します。これは、SQL文の実行機能と、パラメータの置換機能を持っています。

**プリペアードステートメントの取得（prepare）：**
* 変数 = PDOオブジェクト->prepare(SQL文);

```php
<?php

// 用意したSQL文をPDOオブジェクトのprepare関数に渡し、
// プリペアードステートメントを生成する
$pdo_st = $pdo_obj->prepare($sql);

// ここで生成された$pdo_stは
// パラメータを含むSQL文を含み
// DBへのSQL実行機能を持ちます。
```

### ■SQL文のパラメータを置換（bindValue）

プリペアードステートメントの中のSQL文のパラメータ部分を置き換えます。

**パラメータ部分の置換（bindValue）：**

```
    変数 = プリペアードステートメント->
　　　　　　bindValue(パラメータ, 値);
```

**＊プリペアードステートメントを使う利点**
* SQLインジェクションを回避できる
* SQLのテンプレートが生成されるため、値だけ違う同じSQL文を実行する時、速度は圧倒的に速い。

```php
<?php

// プリペアードステートメント内の
// :nameと:ageのパラメータを実際の値で置換
$pdo_st->(':name', 'SEIGA');
$pdo_st->(':age', 29);

// この置換により、
// UPDATE User SET Name = :name WHERE Age = :age
// は、
// UPDATE User SET Name = 'SEIGA' WHERE Age = 29
// となる
```

### ■SQL文の実行

プリペアードステートメントの中で、SQL文が完成しました。後は、実行するだけです。

**SQL文の実行（execute）：**
* 変数 = $pdo_st->execute();

```php
<?php

// プリペアードステートメントのexecute関数を実行
// 晴れて、データベースへSQL文が実行される
$pdo_st->execute();

// UserテーブルのIDが2のレコードのNameが「SEIGA」に

// 最後にPDOオブジェクトを破棄して切断
$pdo_obj = null;
```

### ■（SELECTの場合）実行結果を取得

UPDATE/INSERT/DELETEの場合、execute関数を実施して処理が完了となりますが、SELECTの場合は取得したデータを利用するはずです。そのため、データベースからの結果を収集する処理が必要となります。

データベースからの結果もプリペアードステートメントに格納されているので、取り出します。

**検索結果の取り出し（fetchAll）：**
```
　　変数 = プリペアードステートメント->
　　　　　　fetchAll(PDO::FETCH_ASSOC);
```

fetchAll関数を呼び出すと、取得データを連想配列にして返却してくれます。

```php
<?php

// ユーザーテーブルを全て取得する
$sql = "SELECT * FROM User";
$pdo_st = $pdo_obj->prepare($sql);
$pdo_st->execute();

// 実行結果を連想配列で取得
$datas = $pdo_st->fetchAll(PDO::FETCH_ASSOC);
// 取得結果を見てみましょう
var_dump($datas);

// 最後にPDOオブジェクトを破棄して切断
$pdo_obj = null;
```
