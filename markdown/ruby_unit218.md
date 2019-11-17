# ブラウザでのRuby
### 表示までの流れ

### ■ブラウザへ表示までの流れ

① ブラウザを利用して、Webページをリクエスト
↓
② 対応するページと紐づくRubyのコードを呼び出し

``` HTML
<HTML>
    <head>サンプル</head>
    <body>
        <%= "Hello world !!" %>
    </body>
</HTML>
```

↓
③ Rubyをhtmlに変換

``` HTML
<HTML>
    <head>サンプル</head>
    <body>
        Hello world !!
    </body>
</HTML>
```

↓
④ 出力されたhtmlを送信

&nbsp;
### ①Webページのリクエスト

InternetExplorerやChromeなどのブラウザで、皆さんは見たいサイトへアクセスします。
すると、ブラウザ上部のアドレスバーに、サイトのURLが表示されます。

``` Text
例）http://www.geekjob-sample.co.jp/hello
```

このタイミングで、ブラウザはサーバーに対してWebページのリクエストを行っています。
例の場合、

- www.geekjob-sample.co.jpというドメイン（=IPアドレス）のサーバーへ
- helloというWebページをリクエストする

という意味になります。

&nbsp;
### ②対応するページと紐づくRubyのコードを呼び出し

ブラウザから送られてきたリクエストに応じるため、サーバー上では該当ページがリクエストされます。

今回の例では、**hello**というページがリクエストされます。
ページに対応するファイルとして拡張子rbと、拡張子erbのファイルがそれぞれRubyに読み込まれます。

``` Ruby
#hello_controller.rb
require 'rubygems'
require 'rack'

class HelloController
  def call(env)
    Rack::Response.new(render("hello.html.erb"))
  end

  def render(template)
    path = File.expand_path("../../views/#{template}", __FILE__)
    ERB.new(File.read(path)).result(binding)
  end
end
```

``` HTML
<!-- hello.html.erb -->
<html>
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
  <title>Hello</title>
</head>
<body>
  <%= "Hello, Rack" %>
</body>
</html>
```

&nbsp;
### ③Rubyをhtmlに変換

Rubyのコードをそのままユーザーに送るわけにはいきません。
HTMLに変換してからユーザーに送信する必要があります

この変換はサーバーが行ってくれます。
Rubyの場合は**Rack**という追加機能をインストールすることでRackをサーバーとして動かすことが可能です。

``` HTML
<!-- hello.html.erb -->
<html>
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
  <title>Hello</title>
</head>
<body>
  <%= "Hello, Rack" %>
</body>
</html>
```

---Rackが変換---

``` HTML
<!-- hello.html -->
<html>
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
  <title>Hello</title>
</head>
<body>
  Hello, Rack
</body>
</html>
```

&nbsp;
### ④出力されたHTMLを送信

サーバー側でRubyを処理し、ブラウザが理解できるHTMLを作成しました。

サーバーは、このHTMLのデータをブラウザに送信します。
ブラウザはHTMLのデータを受け取り、その内容に応じて表示を行います。
