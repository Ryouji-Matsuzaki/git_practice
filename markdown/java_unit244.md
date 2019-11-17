# Javaの基礎
## 文字の表示

## ■文字の表示
下記のプログラムは、  
　**こんにちは！**  
　**こんばんは！**  
とブラウザに文字を表示するプログラムです。

Javaで文字を表示する場合、<font color="red">System.out.println</font> を利用します。

　**使い方：**  
　　System.out.println(表示したい文字列);⇦セミコロン

```java
class Hello {
    public static void main( String[] args) {

	System.out.print("こんにちは！");
	System.out.print("こんばんは！");
    }
}

```

## ■文字（文章）の表現

Javaで文字（文章）を表現する場合、

* ダブルクォーテーション『"』

で文字を囲む必要があります。

囲まなかった場合、文字ではなくJavaのプログラムとして処理され、意味不明なプログラムとしてエラーの原因となります。

## ■セミコロン
セミコロン（;）は、命令の区切りを意味します。

```java
System.out.println("こんにちは！");
System.out.println("こんばんは！");
```
上記プログラムでは、

```java
System.out.println("こんにちは！");
```

一つ目の命令。

```java
System.out.println("こんばんは！");
```
二つ目の命令。

Javaは、プログラムを命令毎に理解し、実行します。
