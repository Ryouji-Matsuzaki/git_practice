## 関数
### 戻り値

### ■戻り値

関数は、決まった処理をしてくれるので便利です。しかし、外から処理結果を知る方法がありません。状況によっては、関数の結果で処理を分岐したい場合があります。

そういった場合は、関数に戻り値を実装し、関数の中で処理した結果を呼び出し元に返却しましょう。

```
　戻り値の設定：
　　function 関数名() {
　　　　// 関数の処理
　　　　return 呼び出し元に返したい情報;
　　}
```

戻り値の情報に制限はありません。数字、文字列、配列、何でも返却できます。

```php
<?php
// TODO
```

```php
<?php
// 自分のプロフィールを配列にして返却する関数
function make_profile() {
$infos = array();
$infos['age'] = 34;
$infos['name'] = '添田亮司';
$infos['address'] = '千葉県';
return $infos;
}

// プロフィール関数を呼び出し（戻り値の受け取り）
$myprof = make_profile();
echo $myprof['age'];//ageの利用
echo $myprof['name']; // nameを利用
echo $myprof['address'];//addressの利用
```

### ■return

returnが利用されるのは大抵関数の中ですが、関数の外でも利用が可能です。その場合、returnが出現したタイミングでプログラムの処理が終了します。

関数の中でも同様で、returnに到達すると、それ以降に記述されている処理は実施されません。

そのため、ループ処理のbreakやcontinueの様に、returnも条件分岐と一緒に利用される場合が多いです。

```php
<?php
// 渡された値に「さん、こんにちは！」を付ける関数
function hello($name) {
    return $name . 'さん、こんにちは！';
    // 上の行でreturnされるので、以下は実施されません。
    $name = $name . 'こんばんは！';
}

// helloを呼び出して処理
// 「添田さん、こんにちは！」と表示
echo hello('添田');
return 1;
// 上の行でreturnされているので、処理が終了。
// 以下の処理は実施されません。
echo hello('青木');
```
