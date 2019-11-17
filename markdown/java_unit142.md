# メソッド
## 引数と戻り値

## ■引数と戻り値

メソッドに、引数と戻り値を作成することで、

**メソッドに処理をしてもらい、結果を受け取る**

ことができるようになりました。

プログラミングにおいてメソッドは欠かせないものです。きちんと理解しておきましょう。

```java
// お金と商品代金から、おつりを計算するメソッド
static double otsuri(int hand, int price) {
    return hand - (price * 1.08);
}

public static void main {
    int wallet = 1000;
    int price = 100;

    if (otsuri(wallet, price) > 0) {
        System.out.println("他にも何か購入されますか？");
    } else {
        System.out.println("また、お待ちしております。");
    }
}
```

## ■①メソッドの呼び出し

まず、walletに1000とpriceに100が入った状態で処理が開始します。その後、otsuriメソッドの呼び出しに到達します。

```java
if (otsuri(wallet, price) > 0) {
```

otsuriの引数として、walletとpriceが指定されているので、実際には下記の様に処理されます。

```java
if (otsuri(1000, 100) > 0) {
```

otsuriメソッドの呼び出し場所がif文の中ですが、まずotsuriメソッドが実施されます。

```java
// お金と商品代金から、おつりを計算するメソッド
static double otsuri(int hand, int price) {
    return hand - (price * 1.08);
}  

public static void main(String[] args){
    wallet = 1000;
    price = 100;
    if (otsuri(wallet, price) > 0) {
        System.out.println("他にも何か購入されますか？");
    } else {
        System.out.println("また、お待ちしております。");
    }
}
```

## ■②メソッドの中へ

外でotsuriメソッドが呼ばれ、メソッドの中に処理が移ってきました。

```java
static double otsuri(hand, price) {
```

呼び出しの際に渡された情報は、このメソッドのなかで1000=hand、100=priceに格納されます。
そのため、実際に処理される際は、

```java
static double otsuri(1000, 100) {
```

の状態となります。

そして、メソッドの処理が行われます。

```java
// お金と商品代金から、おつりを計算するメソッド
static double otsuri(int hand, int price) {
    return hand - (price * 1.08);
}  

public static void main(String[] args){
    wallet = 1000;
    price = 100;
    if (otsuri(wallet, price) > 0) {
        System.out.println("他にも何か購入されますか？");
    } else {
        System.out.println("また、お待ちしております。");
    }
}
```


## ■③メソッドの処理

実際にメソッドを処理します。このメソッドは１行しかないので、簡単ですね。

```java
return hand - (price * 1.08);
```

処理がメソッドに移ったタイミングで、handには1000、priceには100が入りました。
するとここの処理は、

```java
return 1000 - (100 * 1.08);
```

となります。

returnがあるので、この計算結果が呼び出し元に返却されます。今回の場合は、 **892** ですね。

```java
// お金と商品代金から、おつりを計算するメソッド
static double otsuri(int hand, int price) {
    return hand - (price * 1.08);
}  

public static void main(String[] args){
    wallet = 1000;
    price = 100;
    if (otsuri(wallet, price) > 0) {
        System.out.println("他にも何か購入されますか？");
    } else {
        System.out.println("また、お待ちしております。");
    }
}
```

## ■④メソッドの結果をもとに処理

メソッドの処理が終わり、呼び出し元に戻りました。

```java
if (otsuri(wallet, price) > 0) {
```

otsuriメソッドは処理され、結果として892が返却されました。なので、メソッドの呼び出し部分が892に入れ替わります。

```java
if (892 > 0) {
```

このif文であれば簡単ですね。

```java
// お金と商品代金から、おつりを計算するメソッド
static double otsuri(int hand, int price) {
    return hand - (price * 1.08);
}  

public static void main(String[] args){
    wallet = 1000;
    price = 100;
    if (otsuri(wallet, price) > 0) {
        System.out.println("他にも何か購入されますか？");
    } else {
        System.out.println("また、お待ちしております。");
    }
}
```

## ■⑤続きを処理

メソッドが処理され、if文が明確になったので、後は残りの処理が実施されます。

```java
if (892 > 0) {
    System.out.println("他にも何か購入されますか？");
} else {
    System.out.println("また、お待ちしております。");
}
```

今回は、「他にも何か購入されますか？」と表示される事がわかりますね。

仮に、①でwalletの値が100だった場合には、おつりがマイナスになるので、「また、お待ちしております。」と表示されます。

```java
// お金と商品代金から、おつりを計算するメソッド
static double otsuri(int hand, int price) {
    return hand - (price * 1.08);
}  

public static void main(String[] args){
    wallet = 1000;
    price = 100;
    if (otsuri(wallet, price) > 0) {
        System.out.println("他にも何か購入されますか？");
    } else {
        System.out.println("また、お待ちしております。");
    }
}
```

## ■メソッドの組み合わせ
メソッドの戻り値を利用して、他のメソッドの実引数として指定することもできます。

メソッドの戻り値が他のメソッドの仮引数と同じ型の場合、実引数として指定することができます。

```java
static void main (String[] args){
    print( getProfile() );
}

static void print(String text){
    System.out.print(text);
}

static String getProfile(){
    return “私の名前は技育助武です!”;
}
```