# クラス
## 初期化処理と後処理

## ■初期処理

クラスには、初期処理と後処理が実装できます。

初期処理はコンストラクタと呼ばれ、インスタンス生成（new）と同時に実行される処理で、利用前の準備などに使用できます。

初期処理は、普通のメソッドの様に実装でき、引数も利用できます。

**初期処理の実装：**

アクセス修飾子 クラス名(引数1, 引数2, …) {  
　　　　// インスタンス生成時に実施すべき事  
　　}  
```
// Sample.javaクラスファイル内
public class Sample {
    private int courseType = 0;
    private String table = "";

    public Sample(int type) {
        // 初期処理で指定されたコースに応じて、テーブル選択
        this.courseType = type;
        if (type == 1) {
            this.table = "t_php";
        } else {
            this.table = "t_java";
        }
    }
}
// Sample s = new Sample(2); -- こうすると、"t_java"に
```

## ■後処理
後処理はデストラクタと呼ばれ、クラスのインスタンスがどこからも到達不能となったタイミングで実施されます。ただし、実施が保証されているものではありません。

**後処理の実装：**

@Override  
　　protected void   finalize() throws   Throwable {  
　　　　// 後処理で実施したい処理  
　　}  

後処理については、実施が保証されていない事を念頭に置いて、処理を記述しましょう。他クラスとの連携処理などを記述した場合、他クラスが先に処理され思わぬ動作をする可能性があるためです。

```
// Sample2クラスファイル内
public class Sample2 {
    // Integerオブジェクトを持って回るフィールド
    private ArrayList<Integer> data = null;

   @Override
    protected void finalize() throws Throwable {
        this.data = null;
    }
}
```
