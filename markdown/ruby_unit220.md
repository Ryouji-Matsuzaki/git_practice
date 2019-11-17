## ブラウザでのRuby
### 複数ページの遷移

### ■複数ページの遷移

2ページ以上のWebアプリを構築してみましょう。
引き続きHelloAppを拡張し、「next_page」というページを作ってみましょう。

1.next_page_controller.rbをcontrollers/に作成してください(hello_controller.rbをコピーして作るのが楽です)

``` Ruby
#next_page_controller.rb
class NextPageController
  def call(env)
    Rack::Response.new(render("next_page.html.erb"))
  end

  def render(template)
    path = File.expand_path("../../views/#{template}", __FILE__)
    ERB.new(File.read(path)).result(binding)
  end
end
```

2.config.ruは下記のように追記

``` Ruby
#config.ru
require './controllers/hello_controller.rb'
require './controllers/next_page_controller.rb'
use Rack::Reloader, 0
Encoding.default_external = 'UTF-8'

map "/" do
  run HelloController.new
end

map "/next_page" do
  run NextPageController.new
end
```
追記箇所

``` Ruby
二行目
require './controllers/next_page_controller.rb'

八～十行目
map "/next_page" do
  run NextPageController.new
end
```

3.下記のような記述のnext_page.html.erbをviews/に作成してください(hello.html.erbをコピーして作るのが楽です)


``` HTML
/*next_page.html.erb*/
<html>
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
  <title>next_page</title>
</head>
<body>
<%= "ここはつぎのページです" %>
</body>
</html>
```

4.hello.html.erbにリンクを追記しrackを再起動。
リンクをクリックすると「ここはつぎのページです」と表示されれば成功です

``` HTML
/*hello.html.erb*/
<body>
<%= "Hello, Rack" %>
<a href="/next_page">つぎのページ</a>
</body>
```

&nbsp;

### ■複数ページの遷移 -解説-
Rubyでページを追加していくには次のような工程を踏む必要があります。

1.「ページ名controller.rb」を**controllers/**に作成

2.作成したcontrollerの**クラス名をページ名の頭文字大文字**に

3.callメソッド内のrenderメソッド引数を「ページ名.html.erb」に

4.config.ruに「ページ名controller.rb」のrequireと、mapを新たに追記しhttp\://localhost:9292/より後ろのURLとして用いたいURLを設定する。

5.「ページ名.html.erb」をviews/に作成する
