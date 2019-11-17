# ループ処理
## while文

## ■while文
while文は**特定の条件を満たす間**繰り返す、ループ処理です。もちろん、回数による制御も可能ですが、回数以外の条件によるループも実現できます。

**while文の使い方：**
```
　　while (条件） {
　　　　// 繰り返したい処理の記述
　　}
```


```java

// keyが「100000」になるまで繰り返す
// ループ回数を表示する
String key = "1";
int count = 0;
while(key.equals("100000") == false) {
    key = key + "0";
    count++;
}

System.out.println(count + "回ループしました！");


```



## ■無限ループの可能性

while文では、条件を満たす限り繰り返します。そのため、条件設定にミスがあると、永久に同じ処理を繰り返す無限ループになります。

例えば、右記のコードはkeyが「A」で始まる事を前提としたプログラムです。「A」でループが開始すると、ループ毎にA⇒B⇒C⇒Dと変化し、keyが「D」になったところでループが終了します。

しかし、プログラムのミスで、keyの中身が「A-D」以外の文字であった場合には、無限ループとなってしまいます。

while文を利用する際は、条件に気をつけましょう。


```java

// keyは事前に定義。 char型
while (key != 'D') {
    switch(key) {
        case 'A':
            System.out.println("GEEK JOB ");
            key='B';
            break;
        case 'B':
            System.out.println("programming ");
            key='C';
            break;
        case 'C':
            System.out.println("camp ");
            key='D';
            break;
    }
}


```
