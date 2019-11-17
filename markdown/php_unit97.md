## クラス
### 初期処理と後処理

### ■初期処理

クラスには、初期処理と後処理が実装できます。

初期処理は、インスタンス生成と同時に実行される処理で、利用前の準備などに使用できます。

初期処理は、普通のメソッドの様に実装でき、引数も利用できます。

```
　初期処理の実装（__construct）：
　　function __construct(引数1, 引数2, …) {
　　　　// インスタンス生成時に実施すべきこと
　　}
```

```php
<?php
class sample {
    private $courseType = 0;
    private $table = '';

    function __construct($type) {
        // 初期処理で指定されたコースに応じて、テーブル選択
        $this->courseType = $type;
        if ($type == 1) {
            $this->table = 't_php';
        } else {
            $this->table = 't_java';
        }
    }
}
$s = new sample(1); // 初期処理でtableが「t_php」に

```

### ■後処理

後処理は、インスタンスが破棄されるタイミングで実施されます。これは、PHPのエンジンが順不同で実施するため、実行されるタイミングは不定です。

```
　後処理の実装（__destruct）：
　　function __destruct() {
　　　　// 後処理で実施したい処理
　　}
```

後処理については、呼び出し順が不同である事を念頭に置いて、処理を記述しましょう。他クラスとの連携処理などを記述した場合、他クラスが先に処理され思わぬ動作をする可能性があるためです。


```php
<?php
class sample2 {
    // PDOオブジェクトを持って回るフィールド
    private $pdo_obj = null;

    function __destruct() {
        // 後処理で必ずPDOを解放する（DB切断）
        $this->pdo_obj = null;
    }
}

```
