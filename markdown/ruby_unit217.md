## 便利なクラス
### ファイル操作編

### ■ファイル操作

Rubyのファイル操作について説明します。

ファイル、とは、テキストファイルや、画像ファイルなどを指します。
そうしたファイルを読み込んだり、編集したりすることができます。
&nbsp;
Rubyのファイル操作の基本的な流れは、

1. **ファイルオープン**
2. **各ファイル操作**
3. **ファイルクローズ**

になります。
&nbsp;
また、ファイル操作には**読み込み・書き込み・追記**のモードが存在します。


### ■Fileクラス

ファイルの操作は、**Fileクラス**を利用します。
試しにテキストファイルを読み込んで、その中の文章を表示してみましょう

ファイルがテキストファイルの場合、以下のようにすることで一度に全文を読み込むことが可能です。

``` Ruby
テキストファイルを全文読み込み:
  変数 = File.read(ファイルへの相対パス)
```

``` Ruby
#text.txt
HelloWorld
HelloWorld2
HelloWorld3
```

``` Ruby
#test.rb(text.txtと同じディレクトリに設置)
text = File.read("text.txt")
print(text)
```

``` Ruby
実行結果:
HelloWorld
HelloWorld2
HelloWorld3
```

#### Tips
テキストファイルの中身が日本語の場合、Windowsのコマンドプロンプトでは文字コード変換をしないと文字化けして表示されてしまいます。
文字コード変換について調べるか、英語でテキストファイルを作りましょう

---

より詳細なファイルの読み込みのためには、以下のように記述する必要があります

``` Ruby
Fileクラスでファイル操作:
  File.open(ファイルへの相対パス) do |io|
    ファイルへの操作
  end
```

ファイルからデータを読み込むには、この「ファイルへの操作」部分でそれに適した記述をする必要があります。

``` Ruby
ファイルへの操作(一行ずつ読み出し):
  io.gets
```

``` Ruby
ファイルへの操作(全行をそれぞれ配列にする):
  io.readlines
```

``` Ruby
#ファイルを読み込んで一行だけ表示(改行文字も読み込まれる)
File.open("text.txt") do |io|
  print(io.gets)
end

#以下のように記述することで全行を読み込み表示することも可
File.open("text.txt") do |io|
  while line = io.gets
    print(line)
  end
end

#三行目だけ表示
File.open("text.txt") do |io|
  lines = io.readlines
  print(lines[2])
end
```

---
ファイルに文字列を追加するなども可能です。
openメソッドに第二引数として「w」や「a」を指定します

``` Ruby
Fileクラスでファイル操作(新規書き込み):
  File.open(ファイルへの相対パス,"w") do |io|
    io.puts(書き込みたいテキスト)
  end
```

ファイルが存在しない場合は新規作成され、存在する場合は上書き保存されます。
ファイルの末尾に追記したい場合は以下のようにします

``` Ruby
Fileクラスでファイル操作(末尾に追記):
  File.open(ファイルへの相対パス,"a") do |io|
    io.puts(書き込みたいテキスト)
  end　
```

``` Ruby
#ファイルに一文を上書き(もともとの内容は削除される)
File.open("text.txt","w") do |io|
  io.puts("HelloHello")
end

#ファイルの末尾に追記する(もともとの内容は保持される)
File.open("text.txt","a") do |io|
  io.puts("addHello")
end
```

``` Ruby
実行結果:
HelloHello
addHello
```
