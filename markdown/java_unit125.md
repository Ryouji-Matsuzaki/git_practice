# 配列
## ArrayListの操作

## ■配列の作成

ArrayListはクラスです。クラスを利用する場合、通常の変数宣言とは少し違い、new演算子を利用して作成します。

**ArrayListによる配列の作成：**
```
　　ArrayList<クラス> 変数名 =
　　　　　　　　　　new ArrayList<クラス>();
```

ArrayListは、作成時に<>の中に指定したクラスを格納する配列となります。クラスにStringを指定したら、文字列しか入りません。Integerを指定したら、整数しか入りません。

また、ArrayListを利用するにはimportが必要になります。

```java
// この1行がimport文
import java.util.ArrayList;

class Challenge {
    public static void main(String[] args){
        // 整数を扱う配列の作成
        ArrayList<Integer> data1 = new ArrayList<Integer>();

        // 文字列を扱う配列の作成
        ArrayList<String> data2 = new ArrayList<String>();
    }
}

```


## ■配列の操作

ArrayListは動的な配列です。そのため、後から要素の増減が可能です。それを行うための機能が用意されているので、ご紹介します。

|操作|説明|
|:-----|:-----|
|add|要素の追加|
|get|要素の取得|
|set|要素の更新|
|remove|要素の削除|
|size|要素数取得|


```java
import java.util.ArrayList;

class Challenge {
    public static void main(String[] args){
        // 配列の作成
        ArrayList<String> data = new ArrayList<String>();

        // 要素の追加
        data.add("添田");
        // 要素の取得 -- 添田が表示される
        System.out.println(data.get(0));
        // 要素の更新 -- 添田が青木に変更される
        data.set(0, "青木");
        // 要素数取得 -- １つの要素（青木）があるので、１と表示
        System.out.println(data.size());
        // 要素の削除 -- 要素の削除は、番号でも実値でも可
        data.remove(0); // data.remove("青木");でも可
    }
}
```
