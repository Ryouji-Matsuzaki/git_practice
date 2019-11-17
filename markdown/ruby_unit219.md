## ブラウザでのRuby
### rackインストール

### ■まずはRackでブラウザに出力してみよう

コンソール画面で、

``` Ruby
gem install rack
```

と入力

Rackのインストールが完了したら、適当なディレクトリに下記の二つのファイルを用意し、

``` Ruby
#hello.rb
require 'rubygems'
require 'rack'
class HelloApp
  def call(env)
    [200, {"Content-Type" => "text/plain"}, ["Hello, Rack"]]
  end
end
```

``` Ruby
#hello.ru
require './hello.rb'
run HelloApp.new
```

そのディレクトリで

``` Ruby
rackup hello.ru
```

と入力します。

ブラウザで**http\://localhost:9292/**にアクセスすると画面に表示されるはずです。

Rack起動中はコンソールの操作ができません。
停止するにはコンソール画面でctrlとcです

&nbsp;

### ■Webアプリとしての形を整えよう
Webアプリとして開発しやすくするための**基本の型**があります
前スライドのコードをその形に置き換えていきましょう

1.次のようなフォルダを作る(スペル注意！)

``` Ruby
■HelloApp
 >■ controllers
 >■ views
```

2.「hello.ru」を「config.ru」に改名し、下記のように改変。HelloApp/に設置

``` Ruby
#hello.ru
require './hello.rb'
run HelloApp.new
```

---ファイル名変更＆コード改変---

``` Ruby
#config.ru
require './controllers/hello_controller.rb'
use Rack::Reloader, 0
Encoding.default_external = 'UTF-8'
map "/" do
  run HelloController.new
end
```

3.「hello.rb」を「hello_controller.rb」に改名し、下記のように改変。controllers/に設置

``` Ruby
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

4.新たに「hello.html.erb」というファイルを作成し、下記のように記述。views/に設置

``` HTML
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

5.コマンドでHelloAppディレクトリに移動し、

``` Ruby
rackup
```

と入力。

**http\://localhost:9292/**にアクセスし、下記のような結果がブラウザに表示されればWebアプリとしての形を整えるのは成功です。

``` Ruby
Hello, Rack
```
