# 標準クラス
## ファイル編

## ■ファイル操作
Javaのファイル操作について説明します。
Javaではファイルやフォルダを操作することが出来ます。
ファイルであれば新規作成や書き込み、読み込みなど、フォルダであればフォルダの中にあるファイル操作を行えます。

ファイル操作の基本的な流れは、

1. **ファイルオープン**
2. **各ファイル操作**
3. **ファイルクローズ（close）**

になります。

また、ファイル操作には **読み込み・書き込み・追記** のモードが存在します。

## ■ファイルオープンとclose、FileWriter
ファイルのオープンは、Fileクラスを利用します。ファイルをクローズするには、closeメソッドを利用します。ファイル操作は、必ず開けたら閉めるようにしましょう。

そして、書き込みはFileWriterクラスを利用します。

　**ファイルを操作のため開く（Fileクラス）：**

　　File 変数名 = new File(ファイルパス);

　**ファイルへ書き込む（FileWriterクラス）：**
  * インスタンス作成
FileWriter 変数名 = new FileWriter(File変数);
  * 書き込み
FileWriter変数.write(書き込む文字列);

```java
// Javaクラスファイル内
import java.io.*;

class Sample {
    public static void main(String[] args) {
        // try{ ... } catch( ... ) { ... } という見慣れない記述がありますが，
        // 「DB操作」の単元で詳しく説明を行います。
      try { 
        // ファイルオープン
        File fp = new File("test.txt");

        // FileWriter作成
        FileWriter fw = new FileWriter(fp);
        // 書き込み
        fw.write("文字を書き込みます！");
        // クローズ
        fw.close();
      } catch( IOException e) {
        System.out.println(e.getMessage());
      }
    }
}
```
## ■ファイルの読み出し
今度は、ファイルから情報を読み出してみましょう。読みだす際も同様にファイルオープンとクローズの流れが必須です。

**ファイルから読み出す（FileReaderクラス）：**  
　　FileReader 変数名 = new FileReader(File変数);

**効率的に読み出す（BufferedReaderクラス）：**  
  * インスタンス作成
      BufferedReader 変数名 = new BufferedReader(FileReader変数);
  * 1行読み出し
      変数名.readLine();
  * 全行読み出し
      while ((String変数 = 変数名.readLine()) != null){
        String変数の表示
      }

```java
// Javaクラスファイル内
import java.io.*;
class Sample {
    public static void main(String[] args) {
      try{
        File fp = new File("test.txt");

        // FileReader作成
        FileReader fr = new FileReader(fp);
        // BufferedReader作成
        BufferedReader br = new BufferedReader(fr);
        // 1行読み出し
        System.out.print(br.readLine());

        br.close();
      } catch (IOException e) {
        System.out.println(e.getMessage());
      }
    }
}
```

## ■追記とファイルのクローズ
先ほどのファイルの書き込みは、上書きでした。すでに書かれている内容へ追記するには、追記モードで書き込む必要があります。

**追記モードで書き込む（FileWriter）：**   
　　FileWriter 変数名 = new FileWriter(File変数, true);    
　　※第二引数をtrueにすると、追記モードに  

また、ファイルのクローズは、読み書きに利用したクラスで実施しているのがわかると思います。

**ファイルのクローズ（closeメソッド）:  **  
  変数名.close();

```java
  // Javaクラスファイル内
import java.io.*;

class Sample {
    public static void main(String[] args) {
      try{
        // ファイルオープン
        File fp = new File("test.txt");

        // FileWriter作成 -- 追記モード
        FileWriter fw = new FileWriter(fp, true);
        // 書き込み
        fw.write("文字を追記してます！");
        // クローズ
        fw.close();
      } catch (IOException e){
        System.out.println(e.getMessage());
      }
    }
}

  ```
