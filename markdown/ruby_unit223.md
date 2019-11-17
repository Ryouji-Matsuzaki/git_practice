## ブラウザでのRuby
### データ操作(フォームから)

### ■ページ間でのデータの受け渡し
ページをまたいでのデータの受け渡しをしたいとき、選択肢は大きく二つあります

**1. HTTPリクエスト情報に埋め込む**
**2. ブラウザやサーバーに保存しておく**

始めに、HTTPリクエスト情報に埋め込む方法として、**フォームからの送信**をやってみましょう

&nbsp;

### ■HTMLの記述

formページとform_requestページの2ページ構成で確認してみましょう。
Rubyで入力内容を利用するには、HTMLの\<body>\</body>の間部分で下記の作業が必要となります。

**HTML部分で実施する事：**

- 入力項目へ名前を付ける(name属性の利用)
- 入力項目をformタグで括る
- formタグのaction先を指定する
- submitボタンを作成する

入力項目へ名前を付けるには、inputやselect、textareaなどに用意されているname属性を利用します。
Rubyではこのname属性に設定された名前で入力値を利用する事になります。

---
formタグで括った中にある入力項目の情報がformタグのaction属性に指定されたURLへ転送されます。

下記の例では、action属性に「/form_request」と記述されています。
この場合、利用者が送信ボタン（submit）を押すと、formタグで用意されているinput達に入力された情報は、http\://localhost:9292/form_requestへと送信されます。


```HTML
<form action="/form_request" method="get">
   <!-- formタグで括られた入力項目はこれら -->
   <p>氏名：<input type="text" name="name"></p>
   <p>性別：
   <input type="radio" name="sex" value="male">男
   <input type="radio" name="sex" value="female">女
   </p>
   <p>血液型：<select name="blood_type">
   <option value="A">A型</option>
   <option value="B">B型</option>
   <option value="O">O型</option>
   <option value="AB">AB型</option>
   </select>
   </p>
   <p>自由入力：<br>
   <textarea name="free" rows="5" cols="40"></textarea></p>
   <p><input type="submit" value="送信"><input type="reset" value="リセット"></p>
 </form>
```

&nbsp;

### ■Rubyで受け取り

入力された情報を受け取るには、受け取りたいページに対応するコントローラーで、以下のように記述します。

``` Ruby
パラメータを個別に取得する方法:
  request ＝ Rack::Request.new(env)
  変数=request.params[フォームのname属性値]
```

上記のように記述すると、入力値がそのまま変数に格納されます。
また、一気に情報を取得するならば、

``` Ruby
パラメータを一度に取得する方法:
  request ＝ Rack::Request.new(env)
  変数 = request.params()
```
　　
入力情報は変数にHashとして(キー名はフォームのname属性の値、要素は実際に入力された内容のペア)代入することができます。

``` Ruby
class FormRequestController
  def call(env)

    #リクエスト情報を取得
    request = Rack::Request.new(env)

    #入力情報を個別に取得。
    name = request.params["name"]

    #入力情報すべてを、直接インスタンス変数に代入
    @params = request.params()

    Rack::Response.new(render("form_request.html.erb"))
  end

  def render(template)
    path = File.expand_path("../../views/#{template}", __FILE__)
    ERB.new(File.read(path)).result(binding)
  end
end
```
---
一度に情報を取得し、直接インスタンス変数に格納した場合、インスタンス変数はそのまま対応するERBへと送られますので、下記のように

``` Text
@インスタンス変数名[フォームのname属性の値]
```

とすれば値を取り出すことが可能です。

``` HTML
/*form_request.html.erb*/
<body>
<p><%= @params %></p>
<p>名前は<%=@params["name"]%></p>
<p>性別は<%=@params["sex"]%></p>
<p>血液型は<%=@params["blood_type"]%></p>
<p>自由記述は<%=@params["free"]%></p>
</body>
```

&nbsp;

### ■HTTPリクエスト情報に埋め込む方法について

フォームを利用してHTTPリクエスト情報に埋め込む場合、更に二通りの方法があります。
HTMLフォームのmethodで指定することができる以下の二通りです。

``` HTML
<form action="" method="get">
```

``` HTML
<form action="" method="post">
```

特徴としては以下の通りです。

**get:**

- URLに文字列として直接載せて送信できる
- 受け取り側のページもURLを分解してパラメータを受け取る
- そのため、そのパラメータ付きURLを保存しておけば同じパラメータを再現できる
- ブクマ時の再アクセスのしやすさなどから**検索系のフォーム**にはよくこちらが利用される
- URLをいじればパラメータも直接改造できるため、セキュアな環境には向かない

**post:**

- URLではなく、内部的な一度きり使われるパラメータとして送信される
- リロードや再アクセス時にパラメータが保持されなくなる。よってブクマしても再現できない
- 使いきりのパラメータなので、**個人情報などのセキュアな情報**を登録する際などによく用いられる
