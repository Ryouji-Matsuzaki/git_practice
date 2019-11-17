# 標準クラス
## 日付編

## ■標準クラスとは
Javaには開発に使える様々なクラスが予め用意されています。  
ArrayListやHashMap、Randomなどのクラスもそうですが、他にもたくさんあります。  
これらを標準クラスと呼びます。

そして、標準クラスの中でも良く使うクラスを幾つかご紹介します。  
今回は、日付に関係するクラスを取り上げます。

## ■日付処理
Javaで日付の情報を扱う場合、Date型としての管理か、**タイムスタンプ**(TimeStamp型)と呼ばれる形での管理を行う事になります。

タイムスタンプとは、ある日付以降の総ミリ秒（経過時間を1/1000秒で表現した数字）を管理するものです。

**Date型の作成：**
  * **当日の日時で作成**
  Date 変数名 = new Date();
  * **特定の日時で作成**
  Date 変数名 = new Date(該当タイムスタンプ);

Dateクラスを利用するには、importが必要です。

```
// Javaクラスファイル内
import java.util.Date;

class Sample {
    public static void main(String[] args) {
        // 当日の日時で日付情報を作成
        Date d = new Date();
    }
}
```

Date型はそのまま表示しても、英語による日付表示になります。また、getTimeメソッドを利用するとTimeStampの情報も取得できます。

```
// Javaクラスファイル内
import java.util.Date;

class Sample {
    public static void main(String[] args) {
        // 当日の日時で日付情報を作成
        Date d = new Date();

        // 日付表示 -- 英語表記の日時表示
        System.out.print(d);
        // タイムスタンプ表示
        System.out.print(d.getTime());
    }
}
```

## ■Calendarクラス
任意の日付を処理したい場合に、いちいちTimeStampを作成するのは大変です。そこで、Calendarクラスを利用しましょう。

Calendarクラスは、扱いがちょっと特殊です。

**Calendarクラスの作成：**  
　　Calendar 変数名 = Calendar.getInstance();

Calendarクラスの利用には、getInstanceメソッドを利用します

```
// Javaクラスファイル内
import java.util.Calendar;

class Sample {
    public static void main(String[] args) {
        // カレンダーインスタンスの作成
        Calendar c = Calendar.getInstance();
    }
}

```

Calendarクラスを作っただけでは、任意の日付になりません。日付の設定を行う必要があります。

**Calendarへ任意の日付を設定：**
  * **Date型を直接渡す**  
  カレンダー変数.set(Date型のデータ);
  * **年月日時分秒を指定する**  
  カレンダー変数.set(年, 月, 日, 時, 分, 秒);

カレンダーの日付処理は、月が0～11になっています。1～12だと思って利用すると、日付が変わってしまうので注意しましょう。

```
// Javaクラスファイル内
import java.util.Calendar;

class Sample {
    public static void main(String[] args) {
        // カレンダーインスタンスの作成
        Calendar c = Calendar.getInstance();

        // 2017年8月12日 18時10分33秒
        c.set(2017, 7, 12, 18, 10, 33);
    }
}
```

Calendarクラスから日時情報を取り出す事も可能です。getメソッドに下記のパラメーターを指定する事で、取得できます。

|取得したい情報|指定パラメータ|
|:-|:-|
|年| Calendar.YEAR|
|月|Calendar.MONTH|
|日|Calendar.DAY_OF_MONTH|
|時|Calendar.HOUR_OF_DAY|
|分|Calendar.MINUTE|
|秒|Calendar.SECOND|

```
// Javaクラスファイル内
import java.util.Calendar;

class Sample {
    public static void main(String[] args) {
        // カレンダーインスタンスの作成
        Calendar c = Calendar.getInstance();
        // 2017年8月12日 18時10分33秒
        c.set(2017, 7, 12, 18, 10, 33);

        // 年取得
        System.out.print(c.get(Calendar.YEAR));
    }
}
```

## ■日付を自由にフォーマットする
日付を自由にフォーマットする方法は、複数存在します。１つは、Calendarクラスのgetメソッドを利用して、年月日時分秒の情報をそれぞれ取得して、文字列として連結する方法です。

もう一つが、SimpleDateFormatクラスを利用する方法です。

**SimpleDateFormatクラス生成：**  
SimpleDateFormat 変数名 = new SimpleDateFormat(日付書式);

**Date型を文字列に変換：**  
SimpleDateFormat変数名.format(Dateデータ);

```
// Javaクラスファイル内
import java.util.Date;
import java.text.SimpleDateFormat;

class Sample {
    public static void main(String[] args) {
        // 今日の日付作成
        Date now = new Date();
        // SimpleDateFormat作成
        SimpleDateFormat sdf =
            new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");

        System.out.print(sdf.format(now));
    }
}
```

## ■文字列を日付に変換
ここまでは、日付情報を文字列に変更する手法をご紹介しました。ここでは、逆に文字列を日付に変換する方法をご紹介します。

文字列の日付を日付情報に変換するのも、SimpleDateFormatクラスを利用します。

**SimpleDateFormatを利用して変換：**  
SimpleDateFormat変数.parse(日付文字列);

```
// Javaクラスファイル内
import java.util.Date;
import java.text.SimpleDateFormat;

class Sample {
    public static void main(String[] args) {
        // SimpleDateFormat作成
        SimpleDateFormat sdf =
            new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");

        // Date取得
        Date day = sdf.parse("2017/10/11 12:31:50");
    }
}
```

## ■日付書式
SimpleDateFormatで使用する日付書式に利用できるパターンをご紹介します。

|パターン|意味|
|:-|:-|
|yyyy もしくは yy|年。4文字の時は2017、2文字の時は17。|
|MM|月。|
|dd|月における日。Dと間違えない様に。|
|HH|日の時間。24時間表記。|
|mm|分。|
|ss|秒。|
|D|年における日。|
