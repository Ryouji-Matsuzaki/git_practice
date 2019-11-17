## クラス
### メソッド

### ■メソッドの定義

クラス内のメソッドは、主に次のような定義で宣言できます

``` Ruby
メソッドの定義:
  def メソッド名
    処理
  end
```

``` Ruby
#test_class.rb
class Test
 def hello
    print("Helloworld")
 end
end
```

``` Ruby
#test.rb(test_classと同じディレクトリに)
require './test_class.rb'
test = Test.new
test.hello
```

``` Ruby
実行結果:
Helloworld
```
---
&nbsp;

メソッドにオブジェクトを渡して、その値に従って処理を行ってもらうこともできます。

この渡されるオブジェクトのことを**引数**と呼びます

``` Ruby
引数を利用したメソッド:
  def メソッド名(引数,引数,引数,,,....)
    処理
  end
```

引数の部分にはどんなオブジェクトが渡されるのかがわかりやすい変数名を記述しておきます。

引数の組み合わせ、オブジェクト種類や数に制限はありません。

``` Ruby
#test_class.rb
class Test
  def hikisu(text, array, num)
    print("Helloworld" + text)
    print("引数の配列の#{num}番目は#{array[num]}です")
  end
end
```

``` Ruby
#test.rb(test_classと同じディレクトリに)
require './test_class.rb'
test = Test.new
test.hikisu("こんにちは", ["a", "b", "c", "d"], 2)
```

``` Ruby
実行結果:
Helloworldこんにちは引数の配列の2番目はcです
```
---
&nbsp;

引数の初期値を入力しておくことで、メソッド呼び出し時の引数入力を任意にすることができます

``` Ruby
引数の初期値を利用したメソッド:
  def メソッド名(引数=初期値,引数=初期値,,,,....)
    処理
  end
```

引数を渡さずにメソッドを呼び出すとメソッド内の処理では初期値が利用されます。
引数を渡すと初期値は上書きされます。

通常は隠しパラメータとして扱いたい引数があり、たまにそのパラメータを変更したいときがある場合などに便利です。

``` Ruby
#test_class.rb
class Test
  def hikisu(text, array=["あ", "い", "う", "え"], num=1)
    print("Helloworld" + text)
    print("引数の配列の#{num}番目は#{array[num]}です\n")
  end
end
```

``` Ruby
#test.rb(test_class.rbと同じディレクトリに)
require './test_class.rb'
test = Test.new
test.hikisu("こんにちは") # 初期値に従って処理される
test.hikisu("こんにちは", ["a", "b", "c", "d"], 2) # 初期値を上書きすることも可能
```

``` Ruby
実行結果:
Helloworldこんにちは引数の配列の1番目はいです
Helloworldこんにちは引数の配列の2番目はcです
```
---
&nbsp;

メソッドからオブジェクトを取得することもできます。
そのオブジェクトは**戻り値**と呼ばれます。


``` Ruby
戻り値を利用したメソッド:
  def メソッド名
    処理
    return 戻り値
  end
```

returnという記述は省略することもできます。
その場合は最後に処理されたオブジェクトが返却されます

``` Ruby
return省略:
  def メソッド名
    処理
    戻り値
  end
```

``` Ruby
#test_class.rb
class Test
  def modori
    return "あいうえお"
  end
end
```

``` Ruby
#test.rb(test_class.rbと同じディレクトリに)
require './test_class.rb'
test = Test.new
text = test.modori # 文字列"あいうえお"を取得
print(text)
```

``` Ruby
実行結果:
あいうえお
```
