# 連想配列
## Mapの操作

## ■連想配列の操作

MapもArrayListと同様に動的な配列です。そのため、後から要素の増減が可能です。それを行うための機能が用意されているので、ご紹介します。

|操作|説明|
|:----|:----|
|put|要素の追加・更新|
|get|要素の取得|
|remove|要素の削除|
|size|要素数取得|

```java
import java.util.HashMap;

class Challenge {
    public static void main(String[] args){
        // 連想配列の作成
        HashMap<String, String> prof =
                    new HashMap<String, String>();
        // 要素の追加
        prof.put("name", "添田");
        // 要素の更新 -- 添田を林に
        prof.put("name", "林");
        // 要素の取得 -- Name:林と表示
        System.out.println("Name:" + prof.get("name"));
        // 要素数取得 -- 1つの要素があるので、1と表示
        System.out.println(prof.size());
        // 要素の削除 -- 要素の削除は、キーで。nameを削除。
        prof.remove("name");
    }
}

```

## ■連想配列の用途

連想配列は、キーのクラスをStringにすれば、要素にラベルを付けるイメージで管理が可能です。

そのため、HashMapに１まとまりのデータを格納する管理方法などを実現できます。

さらに、１まとまりのデータを格納したHashMapをArrayListで管理すると、ある種のデータをまとめて管理できるようになります。

ぜひ、ArrayListやHashMapを使いこなせるようになりましょう。


```java
import java.util.HashMap;

class Challenge {
    public static void main(String[] args){
        // ユーザー情報をHashMapにまとめ、ArrayListで管理する
        HashMap<String, String> user1 =
                    new HashMap<String, String>();
        HashMap<String, String> user2 =
                    new HashMap<String, String>();
        // 名前と年齢を格納
        user1.put("name", "添田"); user1.put("age", "34");
        user2.put("name", "石塚"); user2.put("age", "39");
        // ユーザー情報を入れる配列
        ArrayList<HashMap> data = new ArrayList<HashMap>();
        // ユーザー情報格納
        data.add(user1);
        data.add(user2);
    }
}

```

## ■Mapのループ処理

Mapもループ処理が適用できます。しかし、使い方が少し違います。キーと要素のセットで扱うため、Map.Entryを利用します。

**Mapの拡張for文：**

```java
for(Map.Entry<キークラス, 要素クラス> 変数名 :
    配列.entrySet()) {
    // 中身を用いた処理
}
```

連想配列の場合、１回毎にキーワードと中身を一緒に取り出し、キーワード変数と中身用変数にそれぞれセットしてくれます。

配列同様に、ループの回数は配列の情報の数だけになります。



```java
import java.util.*;
class Challenge{
    public static void main(String[] args){
        HashMap<String, String> hMap =
                    new HashMap<String, String>();
        hMap.put("S", "soeda");
        hMap.put("H", "hayashi");


        //拡張for文で処理
        for (Map.Entry<String, String> val: hMap.entrySet()) {
            // 自動で取得した要素を処理
            System.out.println(val.getKey());
            System.out.println("->");
            System.out.println(val.getValue());
            System.out.println("/");
        }
    }
}


```