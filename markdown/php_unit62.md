## 条件分岐
### switch文

### ■switch文

１つの値を対象に、複数の条件によるチェックを実施したい場合、switch文を利用できます。if文でも対処できますが、コードが長くなってしまうため、上手く使い分けましょう。

```
　switch文の形式：
　　switch(チェック対象） {
　　　　case 条件値1:
　　　　　　// 該当した場合の処理
　　　　　　break;
　　　　case 条件値2:
　　　　　　// 該当した場合の処理
　　　　　　break;
　　　　（条件があればさらにcaseを記述）
　　}
```

```php
<?php
// $typeにはスポーツの種類を表す数値が入っています
// 10ならサッカー、20なら野球、30ならラグビー
switch($type) {
    case 10:
        echo 'サッカー';
        break;
    case 20:
        echo '野球';
        break;
    case 30:
        echo 'ラグビー';
        break;
}


```

### ■break

switch文の各caseの後に、「break;」という記述があります。これは、switch文からの離脱を意味します。

例えば、下記のコードにおいて、$typeが20だった場合には、「case 20:」の箇所で一致し、それ以降の処理が行われます。

1. 「case 20:」に該当
2. 「echo '野球';」の処理を実施
3. 「break;」によりswitch終了

switch文において、breakの記述は必須ではありません。breakが無い場合は、以降のcaseも実施します。上記例の場合は、「case 30:」の処理も実施される事になりますね。

```php
<?php
// $typeにはスポーツの種類を表す数値が入っています
// 10ならサッカー、20なら野球、30ならラグビー
switch($type) {
    case 10:
        echo 'サッカー';
        break;
    case 20:
        echo '野球';
        break;
    case 30:
        echo 'ラグビー';
        break;
}
```

### ■default

if文のelse文の様に、switch文も条件に該当しない場合の処理を記述する事が可能です。それがdefaultです。

```
　defaultの利用：
　　switch(チェック対象） {
　　　　case 条件値1:
　　　　　　// 以降処理とcaseの記述
　　　　　　・・・
　　　　default:
　　　　　　// その他の処理を記述
　　　　　　break;
　　}
```


```php
<?php
// $typeには乗り物の種類を表す数値が入っています
// 2なら車、4なら船、それ以外はその他の乗り物
switch($type) {
    case 2:
        echo '車';
        break;
    case 4:
        echo '船';
        break;
    default:
        echo 'その他の乗り物';
        break;
}
```
