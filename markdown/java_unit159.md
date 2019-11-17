#  データ操作
## セッション

## ■セッション
セッションもcookieと同様にweb上でユーザーの情報を管理する仕組みです。
大きく違うのは、データの置き場所を指定できることです。

cookie同様にcookieの中にもデータを配置できますが、cookieにはセッションIDだけを持たせ、データ自体はサーバーにファイルとして保存したり、データベースに書き込んだりする事が可能です。  

これにより、クッキーでデータを管理するよりも安全に重要なデータを保管できるのです。  
重要なデータを管理する場合は、セッションを利用しましょう。

**セッションの保存先として利用できるもの：**
   * クッキー
   * サーバー内のファイル
   * データベース

## ■セッションの利用
Javaでは、javax.servlet.http.HttpSessionインターフェースを利用して、セッションの読み書きを行います。

　**セッションの取得（HttpSession）：**  
　　HttpSession 変数名 = request.getSession();

また、セッションへのデータの出し入れは下記メソッドを利用します。

　**セッションからデータ読み出し（getAttribute）：**  
　　HttpSession変数.getAttribute(名前);

　**セッションへデータの書き込み（setAttribute）：**  
　　HttpSession変数.setAttribute(名前, 情報);

```
// サーブレットクラス内
import javax.servlet.http.HttpSession;
protected void doGet(HttpServletRequest request, HttpServletResponse response) {
    // セッションへ"Data"という名前で"寿司"を登録
    HttpSession hs = request.getSession();

    // セッションへ登録
    hs.setAttribute("Data", "寿司");

    // セッションから情報を取得 -- 寿司
    String lunch = hs.getAttribute("Data");
}
```

## ■クッキーとの違い
セッションはクッキーと違い、ユーザーのパソコンにデータが保存されません。  
そのため、クッキーよりも秘匿情報を扱うのに適しています。  

また、クッキーは、addCookieメソッドで情報をセットしてから反映されるまでにタイムラグが存在しましたが、セッションデータは出し入れをセッションスコープに行うため、変更が即座に反映されます。  
この違いは大きく、勘違いしたまま実装を行うと大きな問題になる可能性があるので、気をつけましょう。

## ■セッションのイメージ
1. （ユーザー→サーバー）SESSIONIDを持ったクッキーが送られる
2. （サーバー内）Javaにより、「SESSIONIDに該当する一時ファイル」が読み書きされる。
3. （サーバー→ユーザー）SESSIONIDを持ったクッキーが送られる

※図がスライドにあるので参照してください。
