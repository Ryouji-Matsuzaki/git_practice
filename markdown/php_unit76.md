## 関数
### requireとinclude

### ■ファイルを参照する

ここまでは同じファイルの中で、関数とそれ以外の処理を記述してきました。

しかし、全てを１つのファイルにまとめていると、どんどんコードが長くなってしまいます。
また、修正を行う際も、同じファイルを同時に複数人がいじる状況が生まれます。

長いコードも、１つのファイルを複数人でいじるのも、ミスを生む要因となります。

この問題を解決するため、PHPでは他のファイルの処理を参照する仕組みが用意されています。

### ■requireとinclude

requireとincludeは、プログラムの実行中にほかのPHPファイルを読み込む命令です。

requireやincludeを利用する事で、読み込んだPHPの中に書かれている処理も利用できます。

**PHPファイルの読み込み（requireもしくはinclude）：**
* require（又はinclude） PHPファイルのパス

requireとincludeの扱いは基本的に同じです。ただし、読み込みに失敗した場合の動作に違いがあります。

**PHPファイルの読み込みに失敗した場合の動作：**
* requireの場合
  * エラーが発生し、そこで処理が終了します。
* includeの場合
  * Warningを発するものの、処理は継続します。


### ■require_onceとinclude_once

requireやincludeは記述があるたびに該当PHPファイルの読み込みが実施されます。
そのため、色々なファイルを読み込んだ事により関数の重複が発生する事があります。

PHPでは、全く同じ関数の多重定義が認められていません。
そのため、requireやincludeを様々なファイルの中で実施していると多重定義により実行出来なくなる可能性があります。その対策に利用できるのが、require_onceとinclude_onceです。

**requice_once（include_once）の使い方：**
* require_once（又はinclude_once） PHPファイルのパス

require_onceは（include_onceも）PHPファイルの読み込み前に、既に読み込まれているかのチェックを行い、既に読み込まれている場合には読み込みません。そのため、多重定義を回避する事ができます。

PHPファイルの読み込みを利用する際は、require_onceをぜひ利用しましょう。


### ■PHPファイル読み込みのサンプル

```PHP
<?php
// test.php
require_once ('hayashi.php');
echo $my_number;
echo '<br>';
my_profile();
```

↑

```php
<?php
// hayashi.php
$my_number=100;

function my_profile(){
	echo "私の名前は林です<br>";
	echo "好きな音楽はジャズ<br>";
	echo "趣味はゲームと旅行です<br>";
}
```
