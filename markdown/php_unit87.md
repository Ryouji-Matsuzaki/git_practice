## データベース基礎
### 基本的なSQL

### ■SQLとは

ここまでは、プログラミングを学習してきましたが、
一旦離れ、SQLというデータベースを操作するための言語を学習します。

SQLとは、RDBの操作を行うための専用言語です。  
データベースへのデータの出し入れは、このSQLを利用して実施します。

まず、SQLの四大命令を学習します。

**SQLの四大命令：**

* **データを参照する**ための命令：**SELECT**
* **データを更新する**ための命令：**UPDATE**
* **データを追加する**ための命令：**INSERT**
* **データを削除する**ための命令：**DELETE**

&nbsp;

### ■SELECT

SELECTはデータベースから情報を取得するための命令です。

``` Text
SELECTの使い方:
  SELECT カラム1, カラム2, カラム3, ... FROM テーブル WHERE 条件;
  ※WHERE以降は省略可能
  ※省略した場合、テーブルの全データを取得
```

``` Text
テーブル名:User

ID　Name　　　Age
---------------
1　 添田亮司　34
2　 林星河　　29
```

上記のUserテーブルを例にすると、

``` MySQL
SELECT ID, Name, Age FROM User;
```

さらに、条件での絞り込みが可能です。  

Ageが29の情報だけを取得したい場合、　

``` MySQL
SELECT ID, Name, Age FROM User WHERE Age = 29;
```

とすると、２番目の「林星河」のレコードが取得できます。

&nbsp;

### ■UPDATE

UPDATEはデータベースの情報を更新する命令です。

``` Text
UPDATEの使い方:
  UPDATE テーブル SET カラム1=値1, カラム2=値2, ... WHERE 条件;
  ※WHERE以降は省略可能
  ※省略した場合、テーブルの全データを更新
```

``` Text
テーブル名:User

ID　Name　　　Age
---------------
1　 添田亮司　34
2　 林星河　　29
```

上記のUserテーブルのageを全部30にするなら、

``` MySQL
UPDATE User SET age = 30;
```

さらに、条件での絞り込みが可能です。

Nameが「添田亮司」の情報だけを更新したい場合、

``` MySQL
UPDATE User SET age = 30 WHERE Name = '添田亮司';
```

とすると、１番目の「添田亮司」のレコードのAgeが30に更新されます。

&nbsp;

### ■INSERT

INSERTはデータベースの情報を追加する命令です。

``` Text
INSERTの使い方:
  INSERT INTO テーブル (カラム1, カラム2, カラム3, …) VALUES (値1, 値2, 値3, …);
  ※カラムの数と値の数は一致する必要があります。
  ※全てのカラムにデータを指定する場合、カラム記述を省略可能
```


``` Text
テーブル名:User

ID　Name　　　Age
---------------
1　 添田亮司　34
2　 林星河　　29
```

上記のUserテーブルにユーザーを追加する場合、

``` MySQL
INSERT INTO User (ID, Name, Age) VALUES (10, '青木仁志', 28);
```

とする事で、新しい情報が追加されます。

``` Text
結果:
ID　Name　　　Age
---------------
1　 添田亮司　34
2　 林星河　　29
10　青木仁志　28
```

&nbsp;

### ■DELETE

DELETEはデータベースの情報を削除する命令です。

``` Text
DELETEの使い方:
  DELETE FROM テーブル WHERE 条件;
  ※WHERE以降は省略可能
  ※省略した場合、テーブルの全データを削除
```

``` Text
テーブル名:User

ID　Name　　　Age
---------------
1　 添田亮司　34
2　 林星河　　29
```

上記のUserテーブルから削除するなら、

``` MySQL
DELETE FROM User;
```

さらに、条件での絞り込みが可能です。

IDが「1」の情報だけを削除したい場合、

``` MySQL
DELETE FROM User WHERE ID = 1;
```

とすると、１番目の「添田亮司」のレコードだけ削除されます。

``` Text
結果:
ID　Name　　　Age
---------------
2　 林星河　　29
```

&nbsp;

### ■WHERE句の指定

データベースへの操作に絞り込みを掛けるための**WHERE句**ですが、条件の指定は多くの方法があります。

良く使う物を幾つかご紹介しますので、自分でも探して利用してみてください。

``` Text
複数条件の指定:
  ◆両方の条件を満たすか？（AND）
    WHERE 条件1 AND 条件2
  ◆どちらかの条件を満たすか？（OR）
    WHERE 条件1 OR 条件2
```

``` Text
テーブル名:Product

ID　Name　　　　 Type　Price　 Count
-------------------------------------
1　 PS4          1    30000   100
2　 Galaxy S7    2    88000   50
3　 Macbook Pro  3    178800  10
```

例）上記テーブルでCountが30以上、もしくはPriceが50000を超えるもの

``` MySQL
SELECT * FROM Product WHERE Count >= 30 OR Price > 50000;
```

※上記SQL文の「\*」は、ワイルドカードと言い、全カラムを意味します。

---

WHERE句で利用できる比較演算子の幾つかをご紹介します。

|演算子　　　　　　|意味　　　　　　　　　　|使い方|
|:----|:----|:----|
|=|左右が等しい|A=B|
|!= もしくは <>|左右が等しくない|A!=B|
|>|左が右より大きい|A>B|
|<|左が右より小さい|A<B|
|>=|左が右以上|A>=B|
|<=|左が右以下|A<=B|
|IN|左は、右に含まれる|A IN (B, C, D, E, F)|
|IS [NOT] NULL|NULL / NULLではない|A IS NULL / A IS NOT NULL|
|LIKE|左は右を含む|A LIKE '%XXX%' （Aは「XXX」を含む。部分一致）|
