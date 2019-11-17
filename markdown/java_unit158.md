#  データ操作
## クッキー

## ■クッキー
**cookie（クッキー）** という名前を聞いた事がある人も多いと思います。ブラウザとは切っても切れない関係にあるものです。

cookieが何をしているかというと、Webページの処理をスムーズにするため、アクセスしたサイト毎の情報を管理しています。

このcookieの情報は、サーバーとブラウザーで相互にやり取りされ、パソコンの中にもcookieの情報が保存されています。

そして、Javaではこのcookieの情報を操作する事が可能です。また、cookieに必要なデータを保存し、次回接続時に流用する事も可能です。

## ■cookieの利用
cookieを操作するには、Cookieクラスを利用します。

　**cookieに情報を書き込む（Cookieクラス）：**
  * Cookie作成（情報の書き込み）
　Cookie 変数名 = new Cookie(名前, 値);
  * 有効期限の設定  
  変数 = Cookie変数.setMaxAge(有効期限);

また、Cookieクラスに情報を設定するだけでは、Cookieには反映されません。response変数にある、addCookieメソッドを使いましょう。

　**cookieに反映：**
　　response.addCookie(Cookie変数)

```Java
// 通常はサーブレットクラスに記述する
protected void doGet(HttpServletRequest request, HttpServletResponse response) {
    response.setContentType("text/html;charset=UTF-8");
    try (PrintWriter out = response.getWriter()) {

        String food = "ichigo";

        // food のインスタンスを Cookie に格納する。
        // この時，インスタンスに "Data" と名前をつける。
        // food の中身の値（"ichigo"）を取り出す際には
          // "Data" を名前指定することになる。
        Cookie c = new Cookie("Data", food);

        // クッキーの登録。
        // 登録した値を扱えるようになるのは
        // 次回アクセス時からです。
        response.addCookie(c);
    }
}

```
Javaでcookieの中身を利用するには、request変数のgetCookiesメソッドを利用します。getCookiesメソッドは、Cookieクラスの配列を返却します。１つ１つチェックし、自分の利用したい情報を探しましょう。

**cookieの中身を取得（getCookies）：**  
　　変数 = request.getCookies();

下のコードを見てみましょう。
「Data」という名前で「ichigo」という値がクッキーに登録されている状態で，その値を取り出す例です。
※ doGet メソッドの try ブロック内に記述します


```Java
// クッキー情報の取得。情報は配列で取得する。
Cookie[] cs = request.getCookies();

// 値が格納されていることの確認（ null チェック）
if (cs != null) {

    // 配列に格納された全てのクッキーを順番に見ていく
    for (int i = 0; i < cs.length; i++) {

        // getName メソッドで，クッキーの名前情報を取り出す
        String cookieName = cs[i].getName();

        // 個々のクッキーの名前情報の値が，"Data" と一致するか判定。
        // 名前は文字列情報であるため， equals メソッドを利用する。
        if (cookieName.equals("Data")) {

            // getValue メソッドで，値を取り出す。
            String cookieValue = cs[i].getValue();

            out.print(cookieValue);
            break;
        }
    }
}

```

## ■cookieの利用（日本語）
cookie に日本語の値を登録するには，エンコード／デコードといった操作が必要です。
ここでは簡単に，次の意味だと考えてください。

* **エンコード：**
    データを通信に適した形に変換すること
 
* **デコード：**
    変換したデータをもとに戻すこと

URLEncoder の encode メソッド，URLDecoder の decode メソッドは，それぞれ引数に次の値を与えます。

* **第一引数：**
    変換したい文字列

* **第二引数：**
    変換の際の文字コード（通常はUTF-8)

```java
response.setContentType("text/html;charset=UTF-8");
PrintWriter out = response.getWriter();

// エンコード済み文字列の生成
String encodedData = URLEncoder.encode("ばなな", "UTF-8");
Cookie c = new Cookie("Data", encodedData);

response.addCookie(c);Cookie[] cs = request.getCookies();

if (cs != null) {
    for (int i=0; i<cs.length; i++) {
        if (cs[i].getName().equals("Data")) {
            String cookieData  = cs[i].getValue();

            // デコード済み文字列の生成
            String decodedData = URLDecoder.decode(cookieData,"UTF-8");
            out.print(decodedData);
            break;
        }
    }
}

```


## ■cookieのタイムラグ
cookieの扱いについて、１点気を付けるべきポイントがあります。  
それは、addCookieメソッドとgetCookiesメソッドが連動していないという点です。

getCookiesメソッドは、利用者がアクセスしたタイミングのcookie情報を返却します。  
addCookieメソッドは、cookieそのものに情報を書き込みます。  
そのため、addCookieメソッドを実施しても、getCookiesメソッドの情報は変化しないのです。

addCookieメソッドの内容が正しく反映されるのは、次回アクセス時になります。  
これがcookieのタイムラグです。

<font color="Red">addCookieメソッドを実施しても、即座に更新されるわけではない</font>と覚えておきましょう。

## ■クッキーの扱い
少し脱線しますが、クッキーの扱いについて。

cookieはユーザーが一度ページを離れても情報をキープできるため、非常に重要な要素です。  
ただし、前述した通り、cookieは利用者のパソコンに保存されます。  
そのため、ネットカフェなど不特定多数がパソコンを利用する環境では、他人のcookieを盗み見て個人の情報を抜き出す事も可能です。

基本的に便利なcookieですが、そこに保管する情報は誰でも見れるものだと考えましょう。  
そして、個人を特定できるような情報（ID/パスワード/住所など）はcookieで扱うのを控えましょう。  
また、cookieの有効期限を設定し、長期にわたり利用されなかった場合は無効とするなども検討しましょう。
