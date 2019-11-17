## ブラウザでのRuby
### データ操作(セッション)

### ■SESSIONを使ったデータ受け渡し

HTTPリクエスト情報ではなく、ブラウザやサーバーに格納して情報を受け渡す方法を学習しましょう。

まずは2ページ分のコントローラーを作成しましょう。
HelloApp/controller/にセッション格納用、取り出し用のコントローラーをそれぞれ作成します。


``` Ruby
#session_instance_controller.rb（一部）
class SessionInstanceController
  def call(env)
    request = Rack::Request.new(env)

    #セッションに文字列を保存
    request.session["test"] = "セッションテスト"

    Rack::Response.new(render("session_instance.html.erb"))
```

``` Ruby
#session_get_controller.rb（一部）
class SessionGetController
  def call(env)
    request = Rack::Request.new(env)

    #セッションに格納されている値を取得＆インスタンス変数に受け渡し
    @test = request.session["test"]

    Rack::Response.new(render("session_get.html.erb"))
```

---
作成したコントローラー達を、下記のようにURLへ割り当てていきましょう。
また、セッションを使うための設定も記述します。

``` Ruby
#config.ru（追記部分）
#URL割り当て用のrubyファイル読み込み
require './controllers/session_instance_controller.rb'
require './controllers/session_get_controller.rb'

# セッションを使うように設定
use Rack::Session::Cookie,
secret: Digest::SHA256.hexdigest(rand.to_s)

#URLを割り当て
map "/session_instance" do
  run SessionInstanceController.new
end

map "/session_get" do
  run SessionGetController.new
end
```
---
コントローラーに対応するビューを作成しましょう。
また、アクセスしやすいように、ルートページにこの2ページへの直リンクを用意しておきましょう。

``` HTML
#session_instance.html.erb（一部）
<p>セッションに格納しました</p>
<p><a href="/session_get">値を表示</a></p>
```

``` HTML
#session_get.html.erb（一部）
<p>セッションから取得した値は<%= @test %>です</p>
<p><a href="/">トップに戻る</a></p>
```

``` HTML
#hello.html.erb（一部）
<p><a href="/session_instance">セッションの動作テスト</a></p>
<p><a href="/session_get">セッションを直接見る</a></p>
```
---

セッションを利用するにはコントローラーにて以下のように記述することで利用できます。

``` text
セッションに格納する方法:
  request ＝ Rack::Request.new(env)
    request.session[キー名] = 格納したい値
```

``` text
セッションから取り出す方法:
  request ＝ Rack::Request.new(env)
    変数など = request.session[キー名]
```

``` Ruby
def call(env)
   request = Rack::Request.new(env)

   #セッションにデータを保存
   request.session["name"] = "山田"

   #セッションに入力パラメータを保存することも可能
   request.session["age"] = request.params["age"]

   #セッションから値を取り出し
   time = request.session["age"]
```

また、config.ruに下記のように記述しておく必要があります。

``` Ruby
#config.ru
use Rack::Session::Cookie,
secret: Digest::SHA256.hexdigest(rand.to_s)
```
#### Tips
config.ruの「secret: ～」の「～」部分は、SHA2という方式でランダムに生み出された暗号文字列を呼び出しています。ここから出力された値を直接設定することもでき、本格的に運用する場合はそちらのほうがよいでしょう。

&nbsp;

### ■SESSIONを利用する方法の特徴

セッションを利用する場合、HTTPリクエスト情報に保存する場合とは次のような違いがあります。

SESSION:

- GETのように、ページの**URLにパラメータは加わらない**
- POSTのように、ページ遷移時のみの受け渡しではないので、何度リロード、再アクセスしても**パラメータを読みだせる**
- Rubyの場合ブラウザ自体に保存されるので、ブラウザ側のデータを削除すると初期化される
- 一定期間で初期化される
- サーバーが再起動すると初期化される。ただし、secretが固定の文字列の場合は再起動しても破棄されない
- 動作が少し遅い
- GETやPOSTと**同時**に利用されることが多く、フォームから受け取ったデータを直後にコントローラーでSESSIONに格納する流れがよくある。特に**2ページ以上**で同じ入力パラメータを参照する必要がある場合、**入力履歴**
などを残しておきたい場合によく利用される。
