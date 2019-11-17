# 条件分岐
## 条件の書き方

## ■比較演算子
if文やelse if文で記述する条件式に利用する、「==」や「>」や「<」などを **比較演算子** と言います。  
それぞれに意味があり、必要なチェックを行うために利用します。

　**比較演算子の種類**
* a == b    ⇒　aとbが等しい事をチェックする式
* a != b    ⇒　aとbが等しくない事をチェックする式
* a < b	    ⇒　aがbより小さい事をチェックする式
* a > b	    ⇒　aがbより大きい事をチェックする式
* a <= b    ⇒　aがb以下である事をチェックする式
* a >= b    ⇒　aがb以上である事をチェックする式

**※文字列の比較**
　文字列を比較する際は、比較演算子ではなくStringに用意されているequalsを使用します。
　a.equals(b) ⇒ aとbの文字列が等しいか比較する式　// a.equals("テスト")といった書き方も可能です

## ■論理演算子
比較演算子だけでも様々な条件をチェックできますが、さらに論理演算子を利用する事で、複雑な条件のチェックが可能になります。

　**論理演算子の種類**
* 条件１ && 条件２  ⇒条件を両方満たす
* 条件１ || 条件２  ⇒条件をどちらか満たす
* !条件1           ⇒条件1を満たさない

他にも論理演算子は数種類あります。興味があれば調べてみましょう。]

```java

int age = 20;
int money = 1000;

// 遊園地の入園料をチェックするif文
// 20歳以上は1000円
// 6歳以上は200円
// 80歳以上と5歳以下は無料
if (age < 6 || age >= 80) {
    System.out.println("無料で入園できます");
} else if (age >= 20 && money >= 1000) {
    System.out.println("大人１名");
    money -= 1000;
} else if (age >=6 && money >= 200) {
    System.out.println("子供１名");
    money -= 200;
} else {
    System.out.println("お金が足りませんでした");
}

```

## ■演算子を利用しない条件式
比較演算子や論理演算子を使って条件式を作る方法以外にも、boolean型変数を使うことでif文を成立させることが可能です。

boolean型変数とは、
「true」か「false」
のどちらかの値しか格納できない変数です。

If文は「条件式の結果がtrueだったら」｛｝内の処理を行いますが、「true」という値が入った変数を条件式に入れることででも同様の結果が得られます。

具体的には下記のように使います。

```java
//boolean型変数「judge」を宣言し、「true」を代入
boolean judge=true;

//変数「judge」の値が「true」の場合はif文内の処理を行う。
if(judge){
	System.out.print("judgeはtrue");
}else{
	System.out.print("judgeはfalse");
}
```

## ■条件の指定について
if文、else文、else if文、さらに論理演算子を利用すると非常に複雑な条件のチェックが可能になります。  
ただし、条件を複雑化してしまうと、プログラムも難解となります。条件を整理し、できる限り複雑な分岐にならない様、心配りをしましょう。

また、どうしても複雑になってしまう場合、分岐箇所に何に関するチェックなのかコメントを残しましょう。

また条件によってif文、else文、else if文の実行結果も変わります。下記のコードを2つを比べてみましょう。

```java
int age = 20;

if ( age > 19) {
    System.out.println("大人です");
} else if ( age > 15) {
    System.out.println("高校生です");
} else if ( age > 12 ) {
    System.out.println("中学生です");
} else if( 12 >= age){
    System.out.println("小学生以下です");
}

```

```java
int age = 20;

if ( age > 19) {
    System.out.println("大人です");
}
if ( age > 15) {
    System.out.println("高校生です");
}
if ( age > 12 ) {
    System.out.println("中学生です");
}
if( 12 >= age){
    System.out.println("小学生以下です");
}

```