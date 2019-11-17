#  データ操作
## 入力内容の取得

## ■入力内容の取得

一般的なWebページでは、ただ情報を表示するだけでなく、利用者に様々な情報を入力してもらっています。
しかし、Webページに入力項目を作っただけでは、入力された情報を利用する事はできません。
Javaで受け取るために、入力部分に設定を行う必要があります。

ここでは、利用者の入力情報をJavaで扱うために必要な

  * HTMLの記述
  * JSPの処理

を学習します。


## ■HTMLの記述
Javaで利用者の入力内容を利用するには、HTML上で下記の作業が必要となります。

**HTML上で実施する事：**
  * 入力項目へ名前を付ける(name属性の利用)
  * 入力項目をformタグで括る
  * formタグのaction先を指定する
  * submitボタンを作成する

入力項目へ名前を付けるには、inputやselect、textareaなどに用意されているname属性を利用します。Javaではこのname属性に設定された名前で、利用者の入力値を利用する事になります。

Javaへ入力内容を送るには、formタグを利用します。formタグで括った中にある入力項目の情報がformタグのaction属性に指定されたURLへ転送されます。

右記の例では、action属性に「./test.jsp」と記述されています。この場合、利用者が送信ボタン（submit）を押すと、inputやselectの利用者の入力情報は、test.jspへ送信されます。

```
<html>
  <head>
    <title>コントロールサンプル</title>
  </head>
  <body>
    <form action="./test.jsp" method="post">
      <!-- formタグで括られた入力項目はこれら -->
      <input type="text" name="txtName">
      <input type="checkbox" name="chkTest">
      <input type="radio" name="rdoSample">
      <input type="button" name="btnTest">
      <input type="submit" name="btnSubmit">

      <select name="cmbList"></select>
      <textarea name="mulText"></textarea>
    </form>
  </body>
</html>
```

## ■Javaの処理
HTMLからsubmitにより送信された情報は、サーバーで受け取り、Javaで利用するためにrequest変数に格納されます。

データを受け取るために、まずは受け取る情報の文字コードを正しいものに指定します。

**文字コードを指定：**
　　requset.setCharacterEncoding(文字コード);

情報を取り出す場合は、下記になります。

**情報の取り出し（getParameterメソッド）：**
　　変数 = request.getParameter(HTMLのname属性値);

```
<%
// 受け取るパラメータの文字コード
request.setCharacterEncoding("UTF-8");
// テキストボックスの情報
out.print(request.getParameter("txtName"));
// チェックボックスの情報
out.print(request.getParameter("chkTest"));
// ラジオボタンの情報
out.print(request.getParameter("rdoSample"));
// ボタンの情報
out.print(request.getParameter("btnTest"));
// コンボボックス（select）の情報
out.print(request.getParameter("cmbList"));
// テキストエリアの情報
out.print(request.getParameter("mulText"));
%>
```
