## ブラウザでのRuby
### ERBファイルの特徴

### ■erb拡張子のついたファイルの特徴

**HTMLファイル**

Rubyでの計算結果などを埋め込むことができない！(静的、記述内容そのままの表示)

``` HTML
<!-- index.html -->
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>Hello</title>
</head>
<body>
<h1>Hello, Rack</h1>
<p>3+4</p>
</body>
</html>
```

``` Text
実行結果（ブラウザ）:
Hello, Rack
3+4 (←計算文をそのまま表示)
```

**ERBファイル**

Rubyでの計算結果などを埋め込むことができる！(動的、記述内容により変化する表示)

``` HTML
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>Hello</title>
</head>
<body>
<h1>Hello, Rack</h1>
<p><%= 3 + 4 %></p>
</body>
</html>
```

``` Text
実行結果（ブラウザ）:
Hello, Rack
7 (←計算結果をそのまま表示)
```

&nbsp;

### ■静的/動的なWebページ

Webページには、動的/静的の２つの種類があります。
ERBは、Rubyで動的なWebページを実現するための技術です。

**静的なWebページ**

* 常に同じ情報を表示するWebページ
* HTMLで構成されている事が多い（.htmlや.htm）
* 表示内容を変更するには、コードを書きなおす必要がある

**動的なWebページ**

* 状況に応じて、必要な情報を自動取得して表示するWebページ
* 動的なWebページを実現するためのプログラミング言語で書かれている
* Webページを表示する際に、必要な情報の収集が行われ、Webページに反映してくれる

&nbsp;

### ■erb拡張子のついたファイルの特徴

erbファイル内では、下記のルールを守ることで、右記のハイライトしてある部分のように、Rubyとしての処理を記述することができます。

``` Ruby
Rubyのコードを処理する:
  <% 処理したいRubyコード %>
```

``` Ruby
Rubyのコードからhtmlへ出力する:
  <%= 出力したい内容 %>
```

<%= ～ %>の記述は、ブラウザへの表示だけでなく、htmlタグ内への出力にも用いることができます

``` Text
<h1>Hello, Rack</h1>
<p>
<% test = 12 %>
<% #複数行にまたがって書くこともできます %>
<%
test2 = 5
test += test2
%>
<%= test %><% #計算結果の17が表示される %>
</p>
<a href="<%= "https://www.google.co.jp/" %>">googleへのリンク</a>
```

``` Text
実行結果（ブラウザ）:
17
googleへのリンク
```

---
下記のように、条件分岐、繰り返し処理などのロジック要素を含むこともできます。


``` Text
<% #条件分岐を仕込むことも可能です %>
<% if 3 > 4 %> <% #条件が偽なので表示されない %>
<p>3は4より大きいです</p>
<% end %>

<% #繰り返し処理を仕込むことも可能です %>
<% 3.times do %>
<p>Hello, Rack</p>
<% end %>
```

``` Text
実行結果（ブラウザ）:
Hello, Rack

Hello, Rack

Hello, Rack
```

条件が成立するときだけHTML要素を表示したり、検索結果の数だけpタグを作る、など動的なページを作るためにはこれらの要素は欠かせません。