## クラス
### メソッドのアクセス制限

### ■メソッドのアクセス制限

クラス内だけで利用したいメソッドや、サブクラスだけで利用したいメソッドなどが存在する場合は、アクセス修飾子によって呼び出せる範囲を制限することができます

``` Ruby
メソッドへのアクセス制限の付与:
  メソッド定義後・・・
  public    :メソッド名
  private   :メソッド名
  protected :メソッド名
```
``` Ruby
# test_class.rb
class Test
  def initialize
    @text = "Helloworld"
  end
  def hello
    print(add_text)
  end
  def add_text
    t = "文字列は" + @text + "です"
    return t
  end
  private :add_text
end
```

こうすることで、インスタンス側で不用意なメソッド呼び出しを防ぐことができます。

&nbsp;

### ■アクセス制限の種類

アクセス制限の種類は、3種類あります。

**アクセス制限:**

- private
 - 同クラス内でのみ利用可能
 - 想定外の利用を回避できる
- protected
 - privateの範囲をサブクラスまでに拡張
- public
 - インスタンス側で利用可能

initializeメソッドを除いてすべてのメソッドはデフォルトでpublicが適応されているので、クラス内でしか利用しないと思われるメソッドを特別に制限するとき以外では記述されません。

アクセス制限が施されている代表的なメソッドとして**initializeメソッドにはprivateが付与されています**(つまりインスタンス名.initializeといった記述ができない)

``` Ruby
#test.rb
require './test_class.rb'
test = Test.new
test.hello
test.add_text
```

``` Ruby
実行結果(privateなメソッド実行部分でエラー)
NoMethodError
```
