## ブラウザでのRuby
### ERBとの連携

### ■ERBとの連携

オブジェクトなどをERBファイルに渡したい場合は、対応するコントローラーにてインスタンス変数を定義することで受け渡すことができます。


``` Ruby
ERBにオブジェクトを受け渡し:
  @インスタンス変数 = オブジェクト
```

インスタンス変数を渡したい場合はRack::Response.new()の記述よりも前に記述する必要があります。

``` Ruby
#hello_controller.rb
require 'rubygems'
require 'rack'

class HelloController
  def call(env)
    @test = "これはtest文字列です"
    Rack::Response.new(render("hello.html.erb"))
  end

  def render(template)
    path = File.expand_path("../../views/#{template}", __FILE__)
    ERB.new(File.read(path)).result(binding)
  end
end
```


``` Ruby
hello.html.erb(bodyタグの間にて):
  <%= @test %>
```
