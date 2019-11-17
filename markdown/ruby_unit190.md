## Rubyの基礎
### 文字の表示

### ■今回の講座のゴール

この講座では以下のようなプログラムの動作を学べます。

``` Text
C:¥workspace> ruby hello.rb
Hello world ← 文字列が表示される
C:¥workspace>
```

&nbsp;

### ■文字の表示
早速Rubyを実行してみましょう

作業ディレクトリに、「hello.rb」というファイルを作成しましょう

hello.rbを開き、以下のようなコードを記述しましょう

``` Ruby
print("Hello world")
```

---

Windowsならコマンドプロンプト、Macならターミナルを起動し、cdコマンドでそのディレクトリに移動しましょう

「ruby hello.rb」と入力してみましょう。画面に「Hello world」と表示されれば成功です

``` Ruby
ruby hello.rb
```

``` Text
C:¥workspace> ruby hello.rb
Hello world
C:¥workspace>
```

&nbsp;

### ■文字の表示とコメントの方法

``` Ruby
コンソールに表示する方法:
  print(表示したいオブジェクト)
```

``` Ruby
コメントを記述する方法:
  # コメント文
```

``` Ruby
print("あいうえお")

# この部分はコメントです。コードに何の影響もありません
# 二行以上のコメントでも文頭にシャープをつける必要あり

print(1) # 1が表示されます
```
