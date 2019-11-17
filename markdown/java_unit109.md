# Javaの基礎
## 表示までの流れ

## ■表示までの流れ

①ブラウザを利用して、Webページをリクエスト  
②コンピュータ上で当該ファイルを探す
```
<HTML>
    <head></head>
    <body>
        <%= "Hello world !!" %>
    </body>
</HTML>

```
③コンピュータ上でJSPをhtmlに変換  
```
<HTML>
    <head>サンプル</head>
    <body>
        Hello world !!
    </body>
</HTML>
```
④出力されたhtmlを取得  
⑤ブラウザへ表示


## ■①Webページのリクエスト

InternetExplorerやChromeなどのブラウザで、皆さんは見たいサイトへアクセスします。  
すると、ブラウザ上部のアドレスバーに、サイトのURLが表示されます。

例）http://www.geekjob-sample.co.jp/access.jsp

このタイミングで、ブラウザはサーバーに対してWebページのリクエストを行っています。  
例の場合、

* www.geekjob-sample.co.jpというドメイン（=IPアドレス）のサーバーへ  
* access.jspというWebページをリクエストする

という意味になります。

## ■②コンピュータ上でファイルを探す
ブラウザから送られてきたリクエストに応じるため、サーバー上では該当ファイルが検索されます。

今回の例では、**access.jsp** というファイルが検索されます。  
見つかったファイルの中身は、以下の様にJavaが記述されています。

```
<HTML>
    <head></head>
    <body>
        <%= "Hello world !!" %>
    </body>
</HTML>
```
## ■③コンピュータ上でjspをhtmlに変換

```
<HTML>
    <head>サンプル</head>
    <body>
        Hello world !!
    </body>
</HTML>
```

## ■④出力されたHTMLを送信
サーバー側でJavaを処理し、ブラウザが理解できるHTMLを作成しました。

サーバーは、このHTMLのデータをブラウザに送信します。  
ブラウザはHTMLのデータを受け取り、その内容に応じて表示を行います。
