# メソッド
## ユーザー定義メソッド

## ■ユーザー定義メソッドとは

下記のように、開発者が自分で定義したメソッドをユーザー定義メソッドと言います。

**ユーザー定義メソッドの作り方：**

```
static 型 メソッド名() {
    // メソッドで実施したい処理
}
```
※ static や void は後の単元で解説されます。今はこれらが必要なものであるとだけ認識しましょう。
※ 型 については次の「戻り値」の単元で学びます

**ユーザー定義メソッドの利用：**

```
    メソッド名();
```

作成したメソッドを利用するには、メソッド名を記述します。

```java

// 同じクラス内
// 自己紹介を表示するメソッド
static String getMyName() {
    String name = "技育";
    name += "助武";

    return name; 
}

public static void main(String[] args){
    // ユーザー定義メソッドの呼び出し
    System.out.println("私の名前は" + getMyName() + "です");
}

```

## ■mainメソッドとの違い

今までの課題ではmainメソッドを作成してきました。
 
ユーザー定義メソッドとmainメソッドはメソッドというくくりでは同じものです。
 
ですが、「クラスではmainメソッドに記述した命令文が実行される」というルールは変わらないため、mainメソッドで作成したユーザー定義メソッドを呼び出さない限り、ユーザー定義メソッドが実行されることはありません。
 

```java
// 同じクラス内
public static void main(String[] args){
    System.out.println("Hello, World!");
}

// mainメソッドで呼び出されていないため実行されない
static String getMyName() {
    String name = "技育";
    name += "助武";

    return name; 
}
```

## ■メソッドの中と外


同じファイル上であっても、メソッドの中と外は全く別次元となります。  
そのため、メソッドの外で宣言した変数は、メソッドの中で利用できません。  
また、メソッドの外で宣言されている変数と同じ変数を作成しても、全く別の扱いを受けます。



```java
// 作成したメソッド
static int getMyAge() {
    int age = 3000;
    return age;
}
```

```java
static void main(String[] args){
    // メソッドを利用
    getMyAge();
    
    // getMyAgeメソッドで定義した変数ageはmainメソッドまで届かずエラーになる
    System.out.println( age );
}
```
