## 関数
### 引数と戻り値

### ■引数と戻り値

関数に、引数と戻り値を作成する事で、

　** 関数に処理をしてもらい、結果を受け取る **

ができるようになりました。

プログラミングにおいて関数は欠かせないものです。きちんと理解しておきましょう。下記のコードを解説していきます。


```php
<?php

// 持ち金と商品代金から、おつりを計算する関数
function otsuri($hand, $price) {
    return $hand - ($price * 1.08);
}

// 関数の外（関数を利用する側）
$wallet = 1000;
$price = 100;

if (otsuri($wallet, $price) > 0) {
    echo '他にも何か購入されますか？';
} else {
    echo 'またのご利用、お待ちしております。';
}

```

### ■①関数の呼び出し


まず、$walletに1000と$priceに100が入った状態で処理が開始します。その後、otsuri関数の呼び出しに到達します。

```
if (otsuri($wallet, $price) > 0) {
```

otsuriの引数として、$walletと$priceが指定されているので、実際には下記の様に処理されます。

```
if (otsuri(1000, 100) > 0) {
```

otsuri関数の呼び出し場所がif文の中ですが、まずotsuri関数が実施されます。


```php
<?php
// 持ち金と商品代金から、おつりを計算する関数
function otsuri($hand, $price) {
    return $hand - ($price * 1.08);
}

// 関数の外（関数を利用する側）
$wallet = 1000;
$price = 100;

if (otsuri($wallet, $price) > 0) {
    echo '他にも何か購入されますか？';
} else {
    echo 'またのご利用、お待ちしております。';
}
```

### ■②関数の中へ

外でotsuri関数が呼ばれ、関数の中に処理が移ってきました。

```
function otsuri($hand, $price) {
```

呼び出しの際に渡された情報は、この関数のなかで1000=$hand、100=$priceに格納されます。
そのため、実際に処理される際は、

```
function otsuri($hand=1000, $price=100) {
```

の状態となります。

そして、関数の処理が行われます。

```php
<?php
// 持ち金と商品代金から、おつりを計算する関数
function otsuri($hand, $price) {
    return $hand - ($price * 1.08);
}

// 関数の外（関数を利用する側）
$wallet = 1000;
$price = 100;

if (otsuri($wallet, $price) > 0) {
    echo '他にも何か購入されますか？';
} else {
    echo 'またのご利用、お待ちしております。';
}

```

### ■③関数の処理

実際に関数を処理します。この関数は１行しかないので、簡単ですね。

```
return $hand - ($price * 1.08);
```

処理が関数に移ったタイミングで、$handには1000、$priceには100が入りました。
するとここの処理は、

```
return 1000 - (100 * 1.08);
```

となります。

returnがあるので、この計算結果が呼び出し元に返却されます。今回の場合は、892ですね。

```php
<?php
// 持ち金と商品代金から、おつりを計算する関数
function otsuri($hand, $price) {
    return $hand - ($price * 1.08);
}

// 関数の外（関数を利用する側）
$wallet = 1000;
$price = 100;

if (otsuri($wallet, $price) > 0) {
    echo '他にも何か購入されますか？';
} else {
    echo 'またのご利用、お待ちしております。';
}

```

### ■④関数の結果を元に処理

関数の処理が終わり、呼び出し元に戻ってきました。

```
if (otsuri($wallet, $price) > 0) {
```

otsuri関数は処理され、結果として892が返却されました。なので、関数の呼び出し部分が892に入れ替わります。

```
if (892 > 0) {
```

このif文であれば簡単ですね。

```php
<?php
// 持ち金と商品代金から、おつりを計算する関数
function otsuri($hand, $price) {
    return $hand - ($price * 1.08);
}

// 関数の外（関数を利用する側）
$wallet = 1000;
$price = 100;

if (otsuri($wallet, $price) > 0) {
    echo '他にも何か購入されますか？';
} else {
    echo 'またのご利用、お待ちしております。';
}

```

### ■⑤続きを処理

関数が処理され、if文が明確になったので、後は残りの処理が実施されます。

```
if (892 > 0) {
    echo '他にも何か購入されますか？';
} else {
    echo 'またのご利用、お待ちしております。';
}
```

今回は、「他にも何か購入されますか？」と表示される事がわかりますね。

仮に、①で$walletの値が100だった場合には、おつりがマイナスになるので、「またのご利用、お待ちしております。」と表示されます。

```php
<?php
// 持ち金と商品代金から、おつりを計算する関数
function otsuri($hand, $price) {
    return $hand - ($price * 1.08);
}

// 関数の外（関数を利用する側）
$wallet = 1000;
$price = 100;

if (otsuri($wallet, $price) > 0) {
    echo '他にも何か購入されますか？';
} else {
    echo 'またのご利用、お待ちしております。';
}

```
