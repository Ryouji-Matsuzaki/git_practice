# 配列
## 配列の操作

## ■配列の操作

配列を操作する場合、配列に情報を入れた時に割り当てられる番号を利用します。

割り当てられる番号は、追加した順に0番から割り当てられます。

```Java

String[] data = {"soeda", "hayashi", "aoki", "koyama"};

// １番目「soeda」を表示
System.out.println(data[0]);
// 2番目「hayashi」を表示
System.out.println(data[1]);
// 3番目「aoki」を表示
System.out.println(data[2]);
// 4番目「koyama」を表示
System.out.println(data[3]);


```


## ■配列の中身の読み書き

最初に中身を詰める事はできましたが、もちろん後から中身を書き換える事も可能です。

**配列の中身を書き換える：**

  * 変数名[番号] = 中に入れたい値

※配列変数がdataという名前の場合
| 操作 | 説明 |
|:----------|------:|
| data[要素番号] | 要素の取得 | 
| data[要素番号] = 情報 | 要素の更新 | 
| data.length | 要素数の取得 || 


```java
String[] data = {"soeda", "hayashi", "aoki", "koyama"};

//0番目の要素「soeda」を取得し、表示する。
System.out.println(data[0])

// 0番目の要素「soeda」を「GEEK JOB」に置き換える
data[0] = "GEEK JOB";

//配列型の変数dataの要素数を取得し、表示する
System.out.println(data.length);

```
