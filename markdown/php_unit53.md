## PHPの基礎
### PHPの記述方法

### ■PHPの記述方法 - 拡張子

PHPを記述するには、「.php」拡張子のファイル名にする必要があります。

　例）test.php

拡張子を「.php」とすることで、サーバーに

**『 このファイルの中身はPHPで書かれてます！ 』**

と示す事になります。

また、大前提として、PHPをインストールしていないと利用できません。


### ■PHPの記述方法 - プログラミング

PHPのプログラムは、

　** <font color="green"><?php<font> ** 　と　** <font color="green">?><font> **

で括られた範囲に記述します。  
下記では、<?php ... ?>で囲まれた部分がPHPのプログラムです。

```php
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <h1>
            <?php
            echo 'Hello world!!';
            ?>
        </h1>
        <?php
            $num = 0;
            for($i=1; $i<=100; $i++) {
                $num += $i;
            }

            echo '1から100まで足すと、' . $num . 'です。';
        ?>
    </body>
</html>
```

そして、他部分は通常のHTMLです。  
PHPはHTMLとの混在を前提としています。

PHPはHTMLと混在させる事が可能ですが、PHPのみの記述ももちろん可能です。

その場合、プログラムの終りを示す <font color="green">?> </font> を省略する事が可能です。

```php
<?php

echo 'GEEK JOB へようこそ！PHPを楽しみましょう！';

// 1-100までを１つ飛ばしで表示します。
for ($i=1; $i<=100; $i+=2) {
    echo $i . '<br>';
}
```
