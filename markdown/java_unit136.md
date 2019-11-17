# サーブレットとJSP
## JavaBeansとは

## ■JavaBeansとは

プログラムの再利用を目的としており、汎用的なロジックで構成されているクラスです。  
また、JavaBeansはリクエストスコープなどに保管することができます。

JavaBeansに求められる条件は、下記です。

**JavaBeansの必要条件：**

* publicで引数無しのコンストラクタ（初期化処理）を持つ
* フィールドは隠匿されていること
* フィールドは命名規則に沿ったメソッドが用意されている（getter/setterを持つ）
* シリアライズ可能であること


## ■publicで引数無しのコンストラクタを持つ

コンストラクタとは、クラスの初期化処理です。クラス名と同じ名前でクラス内に定義できます。

publicで引数無しのコンストラクタをクラス内に作成すれば、１つめの条件はクリアです。

**クラス内に引数無しのコンストラクタを作成：**
```
　　class クラス名 {
　　　　// {}のみで、一切処理なし
　　　　public クラス名() {}
　　}
```

```Java
// Javaクラスに記述した場合です。
// JSPではない事に注意してください。
import java.io.Serializable;

class TestBeans implements Serializable {
    // publicで引数無しのコンストラクタを作成
    // 処理記述なし
    public TestBeans() {}
}
```

## ■フィールドは隠匿されていること

フィールドとは、クラス内に用意する変数の事です。フィールドは隠匿されている事とは、フィールドが外部から利用できない事です。

外部からクラス内の変数を利用できない様にするには、privateを付けて変数の宣言を行いましょう。

**フィールドの隠匿：**
```
　　class クラス名 {
　　　　// フィールド宣言
　　　　private 型 変数名;
　　　　// 初期化ありのフィールド宣言
　　　　private 型 変数名 = 初期値;
　　}
```

```Java
// Javaクラスに記述した場合です。
// JSPではない事に注意してください。
import java.io.Serializable;

class TestBeans implements Serializable {
    // フィールド作成
    private String Name = "";
    // コンストラクタ
    public TestBeans() {}
}
```

## ■getter/setterを持つ

クラス内のフィールドはgetter/setterを持つ必要があります。getter/setterとは、あるフィールドへ情報を出し入れするためのメソッドです。

**getterの命名規則**

* フィールドの型がboolean以外の場合は、「get」で開始し、以降は単語の頭文字を大文字にして宣言する。booleanの場合は、「is」で開始する。

**setterの命名規則**

* 「set」で開始し、以降の単語の頭文字を大文字にして宣言する


```java
// Javaクラスに記述した場合です。
// JSPではない事に注意してください。
import java.io.Serializable;

class TestBeans implements Serializable {
    // フィールド作成
    private String name = "";
    // コンストラクタ
    public TestBeans() {}
    // Nameのgetter
    public getName() { return this.name; }
    // Nameのsetter
    public setName(String n) { this.name = n; }
}
```

## ■シリアライズ可能であること

シリアライズとは、

**メモリ上のデータを変換し、ファイルに保存したり、ネットワークに送信できるようにする事**

です。

Javaではシリアライズ可能にするための記述は１つだけで、クラスにSerializableインターフェースを実装するだけです。

**シリアライズ可能にする：**
```
　　class クラス名 implements Serializable {
　　}
```

また、Serializableインターフェースを実装するには、importが必要になります。

```Java
// Javaクラスに記述した場合です。
// JSPではない事に注意してください。
import java.io.Serializable;
// TestBeansクラスにSerializableを実装しています
class TestBeans implements Serializable {
    // フィールド作成
    private String name = "";
    // コンストラクタ
    public TestBeans() {}
    // Nameのgetter
    public getName() { return this.name; }
    // Nameのsetter
    public setName(String n) { this.name = n; }
}
```
