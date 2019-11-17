## クラス
### 初期化処理とインスタンス変数

### ■インスタンスメソッド

initializeというメソッド名で定義することにより、インスタンス時に自動実行されるメソッドを定義することができます。

``` Ruby
インスタンスメソッドの定義:
  def initialize
    #インスタンス時に行いたい処理
  end
```

``` Ruby
#test_class.rb
class Test
 def initialize
    print("Helloworld")
 end
end
```

``` Ruby
インスタンスメソッド実行タイミング:
  変数 = クラス名.new
```

``` Ruby
#test.rb(test_class.rbと同じディレクトリに)
require './test_class.rb'
test = Test.new
```

``` Ruby
実行結果:
Helloworld
```

上記のコード例のようなprint処理などを実行することはあまりなく、次に紹介するインスタンス変数とセットでよく利用されます 

&nbsp;

### ■インスタンス変数

そのクラスのインスタンス内ならば、メソッドをまたいで値を参照できる**インスタンス変数**というものがあります。

``` Ruby
インスタンス変数の定義:
  @インスタンス変数名 = オブジェクト
```

非常に重要な変数で、オブジェクトの「**属性**」とも呼ばれます。
文字列オブジェクトならば実際の文字列、数値オブジェクトならば数値がこれに該当します。

メソッドにてこの変数に変更が加わった場合は、そのオブジェクトが存在する限りその変更は継続されます。


``` Ruby
# test_class.rb
class Test
  def initialize
    @num = 0
  end
  def add
    @num += 1
  end
  def get_num
    @num
  end
end
```

``` Ruby
# test.rb
require './test_class.rb'
test = Test.new

#addメソッドを10回実行
10.times do
  test.add
end

#@numの現在値を表示
print(test.get_num)
```

``` Ruby
実行結果:
10
```

&nbsp;

### ■インスタンスメソッド本来の使い方

インスタンスメソッドの主な役割として、インスタンス変数を定義するというものがあります。

``` Ruby
インスタンスメソッドでのインスタンス変数定義:
  def initialize(引数...)
　  @インスタンス変数 = オブジェクトor引数
  end
```

``` Ruby
インスタンスメソッドへオブジェクトを渡す:
  変数 = クラス名.new(引数....)
```

逆に、インスタンスメソッド以外ではインスタンス変数を定義することはありません。

@をつけなければメソッド内のみで存在が消去されるローカル変数というものも作成できます。一時的な変数などに用いられます。

``` Ruby
# test_class.rb
class Test
  def initialize(text)
    @num = 10
    @text = text
  end
  def test_print
    i = 5
    print(@num*i)
    print(@text)
  end
end
```

``` Ruby
# test.rb
require './test_class.rb'
test = Test.new("こんにちは")

test.test_print
```

``` Ruby
実行結果:
50こんにちは
```
