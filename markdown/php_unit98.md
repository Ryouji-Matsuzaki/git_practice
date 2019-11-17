## クラス
### 抽象クラス

### ■抽象クラス

抽象クラスは、インスタンスが生成できない特殊なクラスです。

**抽象クラスの特徴：**

* インスタンス生成できない
* 処理が記述されていない抽象メソッドを持つ
* 継承先で抽象メソッドの実装を強制する

```php
<?php
// 抽象クラス
abstract class car {
    // 継承先で実装を強制される抽象メソッド
    abstract protected function engine();
    function run() { … }//共通機能
}

// エラー。インスタンス生成できません。
$kuruma = new car();

```

抽象クラスは、複数人での開発を行う上で非常に有用なクラスです。

多人数で開発を行う場合、ヒューマンエラーによる実装漏れや、実装ミスが発生します。しかし、開発者全員に、抽象クラスの継承を意識させる事で、重要なメソッドの実装漏れを抑制する事ができます。

多人数で開発する場合は、積極的に利用しましょう。


```php
<?php
// carを継承したクラス
class benz extends car {
    private $cartype = '';
    function engine() { … }
    function navi() { … }
}
// carを継承し、engineを実装していないクラス
class ferarri extends car{
    private $cartype = '';
    function expand() { … }
}

$car_b = new benz();
$car_f = new ferarri(); // engineを実装してないのでエラー

```
