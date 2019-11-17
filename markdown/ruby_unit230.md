## DB操作
### RubyによるDB操作のながれ

### ■RubyによるDB操作のながれ

Rubyでデータベースに接続するために、mysql2というgemをインストールしましょう。
コンソール上で

``` Text
gem install mysql2 -v '0.4.5'
```

と入力、mysql2がインストールされるはずです。

動作確認のため、下記のようなコードを持つrbファイルを用意しましょう。

``` Ruby
#db_test.rb
require 'mysql2'

client = Mysql2::Client.new(:host => 'localhost', :username => 'root', :password => '', :database => 'challenge_db')

print("DB connected!")

statement = client.prepare(%q{insert into profiles(profilesID,name,tell,age,birthday) VALUES(?,?,?,?,?)})
statement.execute(6,"山田タロウ","080-1234-5678",56,"1959-12-31")
```

MySQLを起動し、challenge_dbが存在すること、profilesテーブルが存在することを確認しておきましょう。

コンソール画面から、db_test.rbを実行しましょう。
その後、DBのprofilesテーブルに新しいレコードが追加されていれば成功です


---

DB接続の設定として、次の部分が環境により変化します。


``` Text
DB接続の設定部分の記述方法:
Mysql2::Client.new(:host => **ホスト名**, :username =>**ユーザー名**, :password => **パスワード**, :database => **DB名**)
```

**接続が失敗するときなどはよく確認してみましょう。**

上記のインスタンスではClientオブジェクトを獲得できます。

---
Clientオブジェクトを利用することで、SQLを実行することが可能になります。
どのSQL文でも記述が可能です

``` Text
SQLの実行:
  statement =Clientオブジェクト.prepare(%q{?を含むSQL文})
  statement.execute(「？」の個数分の引数)
```

「？」に該当するのは"山田"や080~のように具体的な実数を伴うオブジェクトが存在するときです。
select * table名など特に実数の出番がないSQLを実行するときには

``` Text
SQLの実行(シンプルなSQLの場合):
  Clientオブジェクト.query(%q{SQL文})
```

と一行で表現しても大丈夫です

---

Select文などをRubyで実行した場合は、その結果を検索結果レコード数分の要素を持つ範囲オブジェクト(正確にはMysql2オブジェクトというもの。検索結果レコード数分の範囲を持ち、カラム名をキー、値をバリューとするHashオブジェクトを持つ)で受け取ることができます。

``` Text
SELECTなどの結果を受け取りたいSQLの実行:
  statement =Clientオブジェクト.prepare(%q{?を含むSQL文})
  結果用変数 = statement.execute(「？」の個数分の引数)
```

``` Text
結果を受け取った変数の中身(Hashオブジェクト)の取り出し方:
  結果用変数.each |eachメソッド用の変数名| do
    print(eachメソッド用の変数名["DBのカラム名"])
    など
  end
```

``` Text
SELECTなどの結果から最初の一件だけをHash形式で取得する:
  結果用変数.first
```

&nbsp;

### ■prepareについて

SQL文に『?』を利用し、後から設定をしていますが、なぜなのでしょうか。
それは、悪意ある入力から逃れるためです。

検索などの語句は、ユーザーの入力した条件をそのまま適用する場合が多くあります。
その際に、データベースの知識がある、悪意を持ったユーザーはわざとSQL文を入力するかもしれません。
それをそのまま利用すると、最悪データを破壊される可能性があります。
これを、**SQLインジェクション**と言います。

しかし、prepareメソッドを利用して値を設定すると、入力値をただの文字列として扱う様に変換してからSQL文に適用されます。これにより、データを悪意から守る事ができるのです。

データベースを利用する際は、意識してprepareを利用する様にしましょう。
