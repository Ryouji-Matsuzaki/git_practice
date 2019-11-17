## DB操作
### エラーハンドリング

### ■エラーハンドリングとは

システムが大きくなればなるほど、プログラミングとは別の要因による傷害の可能性が高まります。

データベース操作もその１つで、プログラムが正しく作成されていても、

* ネットワークがダウンしている
* データベースがダウンしている
* 接続情報が間違っている

などの要因で正しく動かない事が想定されます。  
こうなると、プログラム側では正常に動作させるのは難しくなります。

そういった状況へ対処するための施策が、**エラーハンドリング** です。
エラーハンドリングとは、障害（例外という）が発生した時にその例外をハンドリングし、安全にシステムを停止させる手段です。ここでは、データベースへの接続を例にエラーハンドリングを学びます。


### ■DB操作のエラーハンドリング

エラーハンドリングに用いるのは **try-catch-finally** です。

まず、例外の発生が予見される処理をtryで囲みます。

その後に例外が発生した場合に処理を行うcatch部分を実装し、必要であればfinallyを用意します。

```
　エラーハンドリング（try-catch-finally）：
　　try {
　　　　// 例外の発生が予見される処理
　　} catch (例外クラス) {
　　　　// 例外が発生した場合の処理
　　} finally {
　　　　// 例外の有無関係なく、実施したい処理
　　}
```


```php
<?php
// DBの接続処理をエラーハンドリング
try {
    // 接続文字列生成
    $dns =  'mysql:host=localhost;';
    $dns .= 'dbname=Challenge_db;';
    $dns .= 'charset=utf8';

    // データベースへ接続
    $pdo_obj = new PDO($dns, 'hayashi', 'mypassword');

    // 切断
    $pdo_obj = null;
} catch (PDOException $pdo_ex) {
    // 例外発生
    echo 'DB接続に失敗しました。' . $pdo_ex->getMessage();
}

```


### ■PDOのエラーモード設定

PDOは接続時に例外が発生すると、PDOExceptionを発生させますが、SQL文の実行に失敗しても、初期設定では例外を発生させません。

しかし、それでは問題に気が付けない可能性が高いため、PDOのエラーモードを変更しましょう。

**PDOのエラーモード設定（setAttribute）：**
```
　　変数 = PDOオブジェクト->setAttribute(
　　　　　　PDO::ATTR_ERRMODE,
　　　　　　PDO::ERRMODE_EXCEPTION);
```

これで、SQL文の実行に失敗した場合、例外が発生します。

初期のエラーモードは、PDO::ERRMODE_SILENTになっています。


```php
<?php
// 事前に$dnsを宣言済み
try {
    $pdo_obj = new PDO($dns, 'hayashi', 'mypassword');
    // エラーモード設定
    $pdo_obj->setAttribute(PDO::ATTR_ERRMODE,
                         PDO::ERRMODE_EXCEPTION);
    // SQL文生成（存在しないテーブル）
    $sql = 'SELECT * FROM misstable';
    $pdo_st = $pdo_obj->prepare($sql);
    $pdo_st->execute();    // 例外発生
    // … 以下処理省略
} catch (PDOException $pdo_ex) {
    echo 'DB操作で例外が発生。' . $pdo_ex->getMessage();
}
```
