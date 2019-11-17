# サーブレット
## サーブレットクラスとは

## ■サーブレットクラスとは
ブラウザからのリクエストによって実行され、その結果をHTMLで出力します。  
出力されたHTMLは、Webアクセスの結果としてブラウザに表示されます。

1. （ブラウザから）ユーザのアクセス
2. （サーバが）リクエストを処理
3. （サーブレットクラスが）HTMLを返却
4. （サーバが）HTMLを送信

サーブレットクラスを作るには、下記のルールが守られている必要があります。


* javax.servlet.http.HttpServletクラスを継承する  
* doGetメソッドやdoPostメソッドをオーバーライドする
* サーブレット関連クラスをimportする

IDEを利用すると、いずれも自動で実施されます。便利ですね。

## ■javax.servlet.http.HttpServletクラスを継承する

以前作成した、TestServletプロジェクトを使って説明します。

```
public class TestServlet extends HttpServlet

```
という部分が継承部分です。本来なら  
『javax.servlet.http.HttpServlet』  
と記述すべきですが、
```
import javax.servlet.http.HttpServlet;
```
という部分でimportを行っているため、HttpServletというクラス名の記述のみですんでいます。

　**public class TestServlet extends HttpServlet**

「公開クラスであるTestServletは、HttpServletを継承します。」といったところですね。

## ■doGetメソッドやdoPostメソッドをオーバーライドする
一般的にWebアクセスはGetとPostの２種類があります。  
HttpServletにはこの2種類のアクセスを処理するための、**doGet** と **doPost** メソッドが実装されています。

しかし、継承しただけでは **doGet** と **doPost** はHttpServletで処理されてしまうため、独自の処理を実装する事ができません。独自の処理を実装するために、**doGet** と **doPost** を<font color="red">オーバーライド（上書き）</font>します。

オーバーライドするには、

```java
@Override
protected void doGet(HttpServletRequest request, HttpServletResponse response)
        throws ServletException, IOException {

}
```

```java
@Override
protected void doPost(HttpServletRequest request, HttpServletResponse response)
        throws ServletException, IOException {

}
```
上記の様に記載します。NetBeansでサーブレットクラスを作成した場合、自動でdoGetとdoPostの両方をオーバーライドしますが、どちらかだけで処理を考えている場合には、もう片方は処理しない様に変更しましょう。

## ■サーブレット関連クラスをimportする
IDEでは自動でimportしてくれますが、サーブレットクラスで必ずimportする必要があるクラスがいくつかあります。

必須は、次の部分です。

```java
java.io.IOException
javax.servlet.ServletException
javax.servlet.http.HttpServlet
javax.servlet.http.HttpServletRequest
javax.servlet.http.HttpServletResponse
```

『import java.io.PrintWriter;』  
は必須ではありませんが、HTMLへ情報の出力を行うのであれば必要になります。out.printを用いる場合はimportしましょう。
