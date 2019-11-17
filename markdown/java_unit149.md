# クラス
## 抽象クラス

## ■抽象クラス
抽象クラスは、インスタンスが生成できない特殊なクラスです。

**抽象クラスの特徴：**
* インスタンス生成できない
* 処理が記述されていない抽象メソッドを持つ
* 継承先で抽象メソッドの実装を強制する

```java
// Javaクラスファイル内
// 抽象クラス
abstract class Car {
    // 継承先で実装を強制される抽象メソッド
    abstract protected void engine();
    void run() { // 処理実装 }//共通機能
}

// 利用しようとすると。。。
// エラー。インスタンス生成できません。
Car kuruma = new Car();
```

抽象クラスは、複数人での開発を行う上で非常に有用なクラスです。

多人数で開発を行う場合、ヒューマンエラーによる実装漏れや、実装ミスが発生します。しかし、開発者全員に、抽象クラスの継承を意識させる事で、重要なメソッドの実装漏れを抑制する事ができます。

多人数で開発する場合は、積極的に利用しましょう。

```java
// Javaクラスファイル内
// carを継承したクラス
class Benz extends Car {
    private String carType = "";
    void engine() { // 処理を実装 }
    void navi() { // 処理を実装 }
}
// carを継承し、engineを実装していないクラス
class Ferarri extends Car{
    private String carType = "";
    void expand() { // 処理を実装 }
}

// 抽象クラスを継承した、各クラスを利用すると。。。
Benz car_b = new Benz();
Ferarri car_f = new Ferarri(); // engineがないのでエラー
```
