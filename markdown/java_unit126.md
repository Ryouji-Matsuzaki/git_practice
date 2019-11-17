# 連想配列
## Mapとは

## ■Mapとは

配列は、登録した際の番号で情報を管理していました。  
Mapは、番号の代わりにキーとなるデータを指定する事で、情報の管理を行う配列の事です。  
Mapの様な配列を、連想配列と呼びます。


## ■Mapの作り方

MapもArrayListと同じくクラスです。Mapを利用する場合、キーとするデータのクラスと要素となるデータのクラスを指定します。

**HashMapクラスで連想配列を作成する：**
```
　　HashMap<キークラス, 要素クラス> 変数名
　　　= new HashMap<キークラス, 要素クラス>();
```

HasMapクラスもArrayListクラスと同様に、利用する際にはimportが必要になります。



```java
import java.util.HashMap;

class Challenge {
    public static void main(String[] args){

        // 連想配列の作成 -- キーも要素もString
        HashMap<String, String> data1 =
                        new HashMap<String, String>();


        // 連想配列の作成 -- キーがString、要素は数字
        HashMap<String, Integer> data2 =
                        new HashMap<String, Integer>();
    }
}

```
