# サーブレットとJSP
## 占い結果をJSPへ

## ■占いサービスの結果をJSPで表示しよう！

以前作成した占いサービスは、結果表示をサーブレットの中で行っていました。

今回は、サーブレットとJSPの連携を利用して、JSPで表示してみましょう。

## ■１．JavaBeansを作ろう①

サーブレットからJSPへ情報を渡すため、JavaBeansを作成しましょう。

占いパッケージに新しく『ResultData』というクラスを作成してくださいこのJavaBeansをリクエストスコープ経由でJSPで利用します。


## ■１．JavaBeansを作ろう②

では、ResultDataをJavaBeansとして仕上げます。JavaBeansとして扱うため、以下の条件を満たす様に実装しましょう。


1. java.io.Serializableインターフェイスを実装する。

2. Publicで引数の無いコンストラクタを持つ。

3. フィールドは、カプセル化する。

4. フィールドは、publicで命名規則に沿ったgetter/setterを持つ。

※setLuckも作成しましょう。



## ■２．WEB-INFの中にJSPファイルを作成

WEB-INFの下にjspフォルダを作成し、その中にFortuneTellingResult.jspを作成します。

WEB-INFフォルダは、ブラウザからのURL指定では見えない領域なので、いきなりjspファイルを呼び出す事はできません。
（いたずらがされにくいという事です。）



## ■３．サーブレットからJSPを呼び出す①

作成したJavaBeansに結果を設定し、JSPに渡すためにFortuneTellingのコーディングを変更します。

まず、importを設定してください。

```java
import java.util.Date;
import java.util.Random;
import javax.servlet.RequestDispatcher;
import org.camp.servlet.ResultData;
```

* DateとRandomは、占いの処理に。

* RequestDispatcherは、JSPを呼び出すために。

* ResultDataは、作成したJavaBeansです。

それぞれ利用します。


## ■３．サーブレットからJSPを呼び出す②

占いの結果をJSPに送るために、占い結果をリクエストスコープに設定します。


1. 占い結果を持ちまわるため、先ほど作成したResultDataのインスタンスを生成します。

2. ResultDataクラスのsetterを利用し、実施日付と運勢を記録します。

3. request.setAttributeメソッドで、占い結果をリクエストスコープに登録します。

4. RequestDispatcherクラス利用して、ServletクラスからJSPへ処理を移行します。


## ■４．JSPで結果を表示

先ほど作成したJSPファイルを書き換え、リクエストスコープから占い結果を取り出して、表示する様に修正を行います。

WEB-INF\jsp\FortuneTellingResult.jspを開き、
下記の様にコーディングします。

JavaBeansを展開するため、ResultDataクラスをimportし、request.getAttributeメソッドで、リクエストスコープから運勢データを取り出します。

あとは、取り出した占い結果が表示されるように記述しましょう。


```java
<%@page import="org.camp.servlet.ResultData" %>
<%@page contentType="text/html" pageEncoding="UTF-8" %>
<!DOCTYPE html>
<html>
  <head>
  <%
    ResultData data = (ResultData)request.getAttribute("DATA");
  %>
  <meta http-equiv="contentType" content="text/html: charset=UTF-8">
  <title>JSP Page</title>
  </head>
  <body>
  <%
    if(data != null){
      out.print("<h1>あなたの" + data.getD() + "の運勢は、" + data.getLuck() + "です</h1>");
    }
  %>
  </body>
</html>

```
