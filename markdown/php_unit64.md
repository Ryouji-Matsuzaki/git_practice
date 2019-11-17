## 配列
### 配列の操作

### ■配列の操作

配列を操作する場合、配列に情報を入れた時に割り当てられる番号を利用します。

割り当てられる番号は、追加した順に0番から割り当てられます。

```php
<?php

$data = array('soeda', 'hayashi', 'aoki', 'koyama');

// １番目「soeda」を表示
echo $data[0];
// 2番目「hayashi」を表示
echo $data[1];
// 3番目「aoki」を表示
echo $data[2];
// 4番目「koyama」を表示
echo $data[3];
```

### ■配列の中身の読み書き

最初に中身を詰める事はできましたが、もちろん後から中身を書き換える事も可能です。

** 配列の中身を書き換える： **

* 変数名[番号] = 中に入れたい値

また、後から情報を追加する事も可能です。番号を指定せずに、[]のみで情報を渡すと、最後尾に追加されます。

** 配列の最後尾に情報を追加： **

* 変数名[] = 追加したい値



```php
<?php

$data = array('soeda', 'hayashi', 'aoki', 'koyama');

// 「hayashi」を「GEEK JOB」に置き換える
$data[1] = 'GEEK JOB';

// 最後尾に「groove-gear」を追加
$data[] = 'groove-gear';
// 「groove-gear」を表示
// groove-gearは最後尾に追加されているので、５番目
echo $data[4];

```
