## PHPの基礎
### 表示までの流れ

### ■表示までの流れ

利用者

* ブラウザを利用して、Webページをリクエスト

サーバー側

* コンピュータ上で該当ファイルを探す

```php
<HTML>
    <head></head>
    <body>
        <?php echo 'Hello world !!'; ?>
    </body>
</HTML>
```

* コンピュータ上でphpをhtmlに変換

```html
<HTML>
    <head></head>
    <body>
        Hello world !!
    </body>
</HTML>
```

* 出力されたhtmlを利用者に送信


### ■Webページのリクエスト

InternetExplorerやChromeなどのブラウザで、皆さんは見たいサイトへアクセスします。

すると、ブラウザ上部のアドレスバーに、サイトのURLが表示されます。

　例）http://www.geekjob-sample.co.jp/access.php

このタイミングで、ブラウザはサーバーに対してWebページのリクエストを行っています。

例の場合、

* www.geekjob-sample.co.jpというドメイン（=IPアドレス）のサーバーへ
* access.phpというWebページをリクエストする

という意味になります。


### ■コンピュータ上でファイルを探す

ブラウザから送られてきたリクエストに応じるため、サーバー上では該当ファイルが検索されます。

今回の例では、access.phpというファイルが検索されます。見つかったファイルの中身は、以下の様にPHPが記述されています。

```php
<HTML>
    <head></head>
    <body>
        <?php echo 'Hello world !!'; ?>
    </body>
</HTML>
```

### ■コンピュータ上でphpをhtmlに変換

発見したPHPファイルをそのままブラウザに送るわけにはいきません。
ブラウザはPHPで書かれた内容を理解できないからです。

そこで、サーバー上でPHPを解釈し、ブラウザが理解できるHTMLに変換します。
PHPのコードが処理され、内容が全てHTMLになりました。

```html
<HTML>
    <head>サンプル</head>
    <body>
        Hello world !!
    </body>
</HTML>
```
### ■出力されたHTMLを送信

サーバー側でPHPを処理し、ブラウザが理解できるHTMLを作成しました。

サーバーは、このHTMLのデータをブラウザに送信します。ブラウザはHTMLのデータを受け取り、その内容に応じて表示を行います。
