## クラス
### クラスの継承

### ■クラスの継承

クラスには、継承という機能があります。
継承とは、元となるクラスをスーパークラスとすることで、元のクラスのもつ各種定義を引き継げる仕組みです。

``` Ruby
クラスの継承:
class サブクラス名 < スーパークラス名
　# サブクラス特有の定義や拡張
end
```

&nbsp;
スーパークラス・・・親となるクラス
サブクラス・・・子となるクラス。同じメソッド名を使うことで**拡張**することもできる。
その際下記メソッドを使わないと**メソッド完全上書き**になってしまうので注意
&nbsp;

``` Ruby
スーパークラスのメソッドの拡張:
　def スーパークラスに定義してあるメソッド名
    super(メソッドにもともとあった引数)
```

``` Ruby
#test_class.rb
class Human
  def initialize(name,age)
    @name = name
    @age = age
  end
  def say_status
    print("名前は#{@name}です。年齢は#{@age}です")
  end
end
class Teacher < Human
  def initialize(name,age,tantou)
    super(name,age)
    @tantou = tantou
  end
  def say_tantou
    print("担当は#{@tantou}です")
  end
end
```

&nbsp;

### ■継承を利用して作成したクラス

継承を利用して作成したクラスも、普通のクラスと同じ方法で利用します。
インスタンスを生成し、メソッドを呼び出します。

サブクラスではスーパークラスで実装されていたメソッドが利用可能となります。

もちろん、スーパークラス自身のインスタンスも可能です。

``` Ruby
#test.rb
require './test_class.rb'
sensei = Teacher.new("添田",30,"プログラミング")
sensei.say_status
sensei.say_tantou
```

``` Ruby
実行結果:
名前は添田です。年齢は30です担当はプログラミングです
```
