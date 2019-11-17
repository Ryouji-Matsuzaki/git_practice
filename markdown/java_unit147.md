# クラス
## アクセス修飾子

## ■アクセス修飾子とは
アクセス修飾子とは、クラスのフィールドやメソッドの前に付けていた単語の事を指します。アクセス修飾子は、クラス、フィールド、メソッドに対して指定する事が可能です。

　**クラス宣言のアクセス修飾子の付与：**    
　　アクセス修飾子 class クラス名 {  
　　　　アクセス修飾子 フィールド名;    
　　　　アクセス修飾子 戻り値 メソッド名() {    
　　　　　　// メソッドの処理    
　　　　}  
　　}  

なお、publicなクラスは1ファイルに1つしか作成できません。かつ、ファイル名と同名のクラスである必要があります。  

```
// Employee.javaファイル内
public class Employee {
    private String name = "";
    private int age = 0;

    public int id = 0;

    public void setHuman(String n, int a) {
        this.name = n;
        this.age = a;
    }

    private  void initId() {
        this.id = 9999;
    }
}
```


## ■アクセス修飾子の種類

アクセス修飾子の種類は、3種類あります。

**アクセス修飾子：**
* private
  * 同クラス内のみ利用可能
  * フィールドは基本的にこれを指定する
  * 想定外の利用を回避できる

* 指定しない
  * 同パッケージ内のみ利用可能

* protected
  * 同パッケージ内及び継承先でのみ利用可能

* public
  * どこからでも利用可能
  * インスタンス経由でも利用可能

```java
// Sample.javaファイル内
// アクセス修飾子テストクラス
public class Sample {
    private int param1 = 0;
    protected int param2 = 0;
    public int param3 = 0;

    // 自クラスは、全部OK
    public void callTest() {
        this.param1 = 1;
        this.param2 = 1;
        this.param3 = 1;
    }
}
```
  sample2クラスのcallTestSPメソッド内で、param1を呼び出していますが、これは継承元でprivateを指定
  されているため、利用できません。

  下部の「あるクラスのメソッド内で利用」以下は、とあるクラスのメソッド内に実装されていると思ってください。

  sampleクラスのインスタンスを生成し、param1を呼び出しますが、これはprivateなので利用できません。また、param2もprotectedで、呼び出しがインスタンス経由のため、利用できません。

```java
// Javaクラスファイル内
// 継承先
class Sample2 extends Sample {
    public void callTestSP() {
        this.param1 = 10; // エラー。privateは呼べない
        this.param2 = 10;
        this.param3 = 10;
    }
}

// あるクラスのメソッド内で利用
Sample test = new Sample();
test.param1 = 100; // エラー。privateは呼べない
test.param2 = 100; // エラー。protectedも呼べない
test.param3 = 100;
```
