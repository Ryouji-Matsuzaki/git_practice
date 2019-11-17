# Javaの基礎
## クラスの記述方法

## ■クラスの記述方法　- 拡張子
クラスを作成するには、「.java」拡張子のファイル名にする必要があります。
※慣例的にファイル名は英字で、頭文字は大文字にする必要があります。
　例）Test.java

拡張子を「.java」とすることで
　『 このファイルの中身はjavaで書かれてます！ 』
と示す事になります。


## ■クラスの記述方法　- プログラミング
クラスでのプログラムは、
<font color="Green">
public static void main(String[] args){    }
</font>  
の { } で指定されている範囲に記述します。

これはmainメソッドと言い、プログラムを実行したときに最初に実行されるコードを記述する箇所になります。
このmainメソッドから連鎖的に処理が始まるため、ここに処理の命令を記述することでソースコードが実行されることになります。


```java
class Test {
	public static void main(String[] args) {

		System.out.println("Hello, World");

	}
}
```
## ■クラスの記述方法　- プログラミング
実行したい処理にはmainメソッドが必要なため、mainメソッドの外や、mainメソッドがない状態でプログラムを記述するとコンパイル時にエラーになることがあります。

```java
class Test {
	System.out.println("これはエラーになります");

    public static void main(String[] args){

    }

}


```
