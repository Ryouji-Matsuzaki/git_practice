# 配列
## ArrayListとは

## ■ArrayListとは

ArrayListとは、Javaに用意されている動的な配列を実現する型（クラス）です。
対して、変数宣言時に[]を使用して作成する配列は、静的な配列です。

**配列の種類：**

* 静的な配列

  * 作成後に要素数を増減できない配列


* 動的な配列

  * 後から要素数を増減できる配列

ArrayListは、後からいくらでも情報を追加・削除できる非常に便利な配列です。  
是非、使いこなせる様になりましょう。



## ■ArrayListに入れられるもの

ArrayListに入れられるのは、クラスのみです。intやdoubleなどの型は利用できません。

しかし、実際にはintやdoubleの値をArrayListで扱いたいシーンは多くあります。

そのため、各型に対応したクラスが用意されています。

|型|対応しているクラス|
|:-----|:-----|
|boolean|Boolean|
|char|Character|
|byte|Byte|
|short|Short|
|int|Integer|
|long|Long|
|float|Float|
|double|Double|
