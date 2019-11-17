## クラス
### アクセス修飾子

### ■アクセス修飾子とは

アクセス修飾子とは、クラスのフィールドやメソッドの前に付けていた単語の事を指します。アクセス修飾子は、フィールド、メソッドに対して指定する事が可能です。

```
　クラス宣言のアクセス修飾子の付与：
　　class クラス名 {
　　　　アクセス修飾子 フィールド名;
　　　　アクセス修飾子 function メソッド名() {
　　　　　　// メソッドの処理
　　　　}
　　}
```

```php
<?php

class Employee {
    private $name = '';
    private $age = 0;

    public $id = 0;

    public function setHuman($n, $a) {
        $this->name = $n;
        $this->age = $a;
    }

    private  function initId() {
        $this->id = 9999;
    }
}

```

### ■アクセス修飾子の種類

アクセス修飾子の種類は、3種類あります。

アクセス修飾子：

* private

  * 同クラス内のみ利用可能
  * フィールドは基本的にこれを指定する
  * 想定外の利用を回避できる


* protected

  * 同クラス及び継承先でのみ利用可能


* public

  * どこからでも利用可能
  * 何も修飾子が無い場合は、これになる
  * インスタンス経由でも利用可能


```php
<?php
// アクセス修飾子テストクラス
class sample {
    private $param1 = 0;
    protected $param2 = 0;
    public $param3 = 0;

    // 自クラスは、全部OK
    public function callTest() {
        $this->param1 = 1;
        $this->param2= 1;
        $this->param3 = 1;
    }
}

```

sample2クラスのcallTestSPメソッド内で、param1を呼び出していますが、これは継承元でprivateを指定されているため、利用できません。

下部の「インスタンス経由」以下は、インスタンスを生成した場合の検証です。

sampleクラスのインスタンスを生成し、param1を呼び出しますが、これはprivateなので利用できません。また、param2もprotectedで、呼び出しがインスタンス経由のため、利用できません。

```php
<?php
// 継承先
class sample2 extends sample {
    function callTestSP() {
        $this->param1 = 10; // エラー。privateは呼べない
        $this->param2 = 10;
        $this->param3 = 10;
    }
}

// インスタンス経由
$test = new sample();
$test->param1 = 100; // エラー。privateは呼べない
$test->param2 = 100; // エラー。protectedも呼べない
$test->param3 = 100;
```
