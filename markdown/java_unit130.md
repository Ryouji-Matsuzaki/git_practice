# ループ処理
## 拡張for文

## ■拡張for文
拡張for文もループ処理の構文ですが、この構文は**配列**を対象とした構文です。

**拡張for文の使い方：**

```java
//◆配列の場合
for(中身を受け取る変数 : 配列) {
    // 中身を利用した処理
}
```

拡張for文は配列の中身を１つずつ取り出し、中身を受け取る変数にセットしてくれます。

また、ループの回数も配列の情報の数に合わせて実施してくれるため、回数カウントなど不要です。


```java

// 数値配列
int[] data1 = {100, 200, 300};

// 配列の中の数字を全て合計する処理です
int total = 0;
for(int value: data1) {
    total = total + value;
}
System.out.println(total);

// 数値配列 -- ArrayListも同じ方法でループ処理できます
// ArrayList<Integer> data2 = new ArrayList<Integer>();


```


## ■配列を普通のfor文で処理

静的配列（[   ]で宣言したもの）やArrayListは、通常のfor文でも処理が可能です。

その場合、for文の中で要素番号を順番に指定する事でループ処理が可能です。

```java

ArrayList<String> al = new ArrayList<String>();
al.add("ABC");
al.add("DEF");

// 通常のfor文で処理
for (int i = 0; i < al.size(); i++) {
    // 配列からi番目の要素を取得
    System.out.println(al.get(i));
}

// 数値配列 -- 静的配列も同じ方法でループ処理できます
// String name[] = {"Hello", "Hi", "Hey"};

```
