# DB操作

## JDBCによるDB操作


## ■データベース操作①
実際にデータベースに接続するコードを書きましょう。

まずは、データベース操作に利用するクラスをインポートします。  
java.sqlパッケージ以下に利用するクラスが固まっているので、  
ワイルドカードで一度にインポートしてしまいましょう。  
```
import java.sql.*;
```

## ■データベース操作②
データベースへ接続します。  

* ⑴Class.forNameメソッドを利用し、libフォルダにあるMysql用のJDBCドライバのインスタンスを生成します。このインスタンスは、生成と同時にDriverManagerにセットされます。

* ⑵DriverManagerのgetConnectionメソッドで、DBへの接続を取得します。
接続情報は、Connectionクラスとして返却されるため、Connectionクラスの変数で受けます。 
※接続時にserverTimezoneのエラーが発生する場合、
    jdbc:mysql://localhost:3306/データベース名?serverTimezone=JST
としてください

```
Connection db_con = null;

try {
  ⑴Class.forName("com.mysql.jdbc.Driver").newInstance();  
  ⑵db_con = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "");
}
```


## ■接続文字列

**DriverManagerによる接続（getConnectionメソッド）：**

* Connection変数 = DriverManager.getConnection(接続文字列, アカウント名, パスワード);  

DriverManagerのgetConnectionメソッドで接続をする際に、必要な接続文字列の内容は下記になっています。  

**接続文字列の構成：**

* "jdbc:" + **データベースの種類** + "://" + **接続先** + ":" + **ポート番号** + "/" + **データベース名**

例) jdbc:**mysql://localhost:3306/test** ⇒ localhostの3306ポートで動いているMySQLのtestというDB  


さらに、接続文字列には文字コードなどを指定するオプションも用意されています。  
ぜひ、調べてみてください。  


## ■データベース操作③
データベースに接続したら、SQL文を実行するためにPreparedStatementを取得しましょう。  

* ⑶ConnectionのprepareStatementメソッドにSQL文を渡します。  
この時、SQL文の中に条件となる値の代わりに『?』を配置します。  
さらに、prepareStatementメソッドの戻り値を受け取りましょう。  

* ⑷prepareStatementメソッドから受け取ったPreparedStatementに対し、  
『?』部分に適用する情報を設定していきます。  
下記の場合、１番目の『?』に対して、33を設定する処理です。

```
PreparedStatement db_st = null;

//中略

⑶db_st = db_con.prepareStatement("select * from sample where age = ?");
⑷db_st.setInt(1, 33);
```  


## ■PreparedStatement

** PreparedStatementの取得（prepareStatementメソッド）：**

* PreparedStatement変数 = Connection変数.prepareStatement(?を含むSQL文);  
    ※?を含まないSQL文でも可能です。  

** 『?』の置き換え（set○○メソッド）：**

  * **整数を設定する場合（setInt）**  
PreparedStatement変数.setInt(何番目の?か, ?に設定する整数);

良く使うset○○を下記に一覧しました。参考にしてください。


| メソッド | 用途 |
|:--------|--------:|
| setInt | 整数を設定 |
| setBoolean | 真偽値を設定 |
| setDate | 日付を設定 |
| setString | 文字列を指定 |


## ■データベース操作④
PreparedStatementに必要な設定を行ったら、SQL文を実行します。

* PreparedStatementのexecuteQueryメソッドを実行します。  
『?』が実際の値に置き換わったSQL文がデータベースに実行されます。  
executeQueryの場合、実行結果をResultSetとして返却してくれます。  
受け取りましょう。  

* ResultSetからSQLの実行結果を取り出し、表示します。  
nextメソッドで、データの有無を確認し、while文でデータがある限り取得し続けています。  
getStringメソッドは、１行のデータからnameカラムの情報を文字列として取得しています。  

```
ResultSet db_data = null;

//中略

⑸db_data = db_st.executeQuery();
⑹while(db_data.next()){
  out.print("名前：" + db_data.getString("name") + "<br>");
}
```


## ■ResultSet
**SQL文の実行（executeQueryメソッド）：**

* ResultSet変数 = PreparedStatement変数.executeQuery();  

**ResultSetのデータの有無をチェック（nextメソッド）：**

* 変数 = ResultSet変数.next();  
※データがある場合はtrue、無い場合はfalseを返却します。  

**ResultSetから特定のカラムの情報を取得（get○○メソッド）：**  

**◆特定のカラムから文字列を取得する**  
* 変数 = ResultSet変数.getString(カラム名);  

良く使うget○○を下記に一覧しました。参考にしてください。

| メソッド | 用途 |
|:--------|--------:|
| getInt | 整数で取得 |
| getBoolean | 真偽値で取得 |
| getDate | 日付で取得 |
| getString | 文字列で取得 |
| getRow | 行番号を取得 |


## ■データベース操作⑤
データベースへの操作が完了したら、最後は使わなくなったものをクローズしましょう。

```
db_data.close();
db_st.close();
db_con.close();
```

データベースへの同時接続数は制限があるため、必ずクローズしましょう。  

また、SQL文を実行する際にexecuteQueryメソッドを実施していましたが、  
INSERT/UPDATE/DELETEの場合はexecuteUpdateメソッドを利用しましょう。  

**INSERT/UPDATE/DELETEの場合（executeUpdate)：**  

* 変数 = PreparedStatement変数.executeUpdate();  
※executeUpdateを実行すると、SQLにより更新された行数が返却されます。  


## ■ソースコード全体
※該当スライドを参照してください。
## ■PreparedStatementについて

SQL文のWhere句部分に『?』を利用し、後から設定をしていますが、なぜなのでしょうか。  
それは、悪意ある入力から逃れるためです。  

検索などのWhere句は、ユーザーの入力した条件をそのまま適用する場合が多くあります。  
その際に、データベースの知識がある、悪意を持ったユーザーはわざとSQL文を入力するかもしれません。  
それをそのまま利用すると、最悪データを破壊される可能性があります。  
これを、**SQLインジェクション** と言います。  

しかし、PreparedStatementのset○○メソッドを利用して値を設定すると、入力値をただの文字列として扱う様に変換してからSQL文に適用されます。これにより、データを悪意から守る事ができるのです。  

データベースを利用する際は、意識してPreparedStatementを利用する様にしましょう。  
