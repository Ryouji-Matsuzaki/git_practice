# Javaの基礎
## JSPの記述方法

## ■JSPの記述方法　- 拡張子
JSPを作成するには、「.jsp」拡張子のファイル名にする必要があります。

　例）test.jsp

拡張子を「.jsp」とすることで、サーバーに  
　『 このファイルの中身はJSPで書かれてます！ 』  
と示す事になります。

また、大前提として、JavaのSDKをインストールしていないと動きません。  
（NetBeansのセットアップができていれば問題ありません）


## ■JSPの記述方法　- プログラミング
JSPのプログラムは、
<font color="Green">
<%　と　%>
</font>  
で括られた範囲に記述します。
下記では、<font color="Green">緑字</font>部分がJavaのプログラムです。

また、<font color="Orange">橙色</font>部分は通常のHTMLです。  
JSPはHTMLとの混在を前提としています。

```
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <h1>
            <%= "Hello world!!" %>
        </h1>
        <%
            int num = 0;
            for(int i=1; i<=100; i++) {
                num += i;
            }

            out.print("1から100まで足すと" + num + "です。");
        %>
    </body>
</html>

```
## ■JSPの記述方法　- プログラミング
JSPはHTMLと混在させる事が可能ですが、Javaのみの記述ももちろん可能です。

また、単純に何かを表示したい場合、  
　<%= 表示したい内容 %>  
と記述する事で、直接表示できます。

```
<%

out.print("GEEK JOB へようこそ！Javaを楽しみましょう！");

// 1-100までを１つ飛ばしで表示します。
for (int i=1; i<=100; i+=2) {
    out.print(i + "<br>");
}

%>

<%--　この記号はコメントになります。　--%>

<%= "直接表示ですよ！" %>
```
