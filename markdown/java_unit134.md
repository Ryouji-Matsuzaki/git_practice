# サーブレット
## 占いサービスを作ってみよう！

## ■占いサービスを作ってみよう！
※実際の作業画面がスライドに載っています。参照してください

サーブレットクラスを利用して、占いサービスを作ってみましょう！

NetBeansで『org.camp.servlet』というパッケージの中にFortuneTellingというサーブレットクラスを作成します。

サーブレットクラスを作成すると、最初から<font color="blue">doGet</font>と<font color="blue">doPost</font>がオーバーライドされています。doPostではdoGetが呼び出されています。

なので、今回は<font color="red">doGet</font>に処理を追加していきます。

※NetBeansの場合は、doGetとdoPostがサーブレットクラス作成時にオーバーライドされており、どちらもprocessRequestが呼ばれています。そのため、processRequestに処理を追加していきます。

## ■占いサービスを組み立てる①
以下を参考にしてdoGetメソッド内に必要な文を記述してください。(NetBeansを使用している方はprocessRequest内に注目してください。)

**【Eclipseの場合】**

```
protected void doGet(HttpServletRequest request, HttpServletResponse response)
        throws ServletException, IOException {
    ⑴response.setContentType("text/html;charset=UTF-8");
    ⑵try (PrintWriter out = response.getWriter()) {
        ⑶
        out.println("Hello, World!");
    }
}
```
　
**【NetBeansの場合】**


```
protected void processRequest(HttpServletRequest request, HttpServletResponse response)
        throws ServletException, IOException {
    ⑴response.setContentType("text/html;charset=UTF-8");
    ⑵try (PrintWriter out = response.getWriter()) {
        ⑶/* TODO output your page here. You may use following sample code. */
        out.println("<!DOCTYPE html>");
        out.println("<html>");
        out.println("<head>");
        out.println("<title>Servlet NewServlet</title>");            
        out.println("</head>");
        out.println("<body>");
        out.println("<h1>Servlet NewServlet at " + request.getContextPath() + "</h1>");
        out.println("</body>");
        out.println("</html>");
    }
}
```
　
⑴これは、ブラウザに返すWebページの文字コードを指定します。NetBeansではデフォルトでUTF-8を指定していますね。
　
⑵これは、Webページを出力するためのクラスを生成しています。JSPでout.printとやっていましたがサーブレットで使うoutはここで生成します。NetBeansではサーブレットクラス作成時に自動で生成していますね。
　
⑶コメントにもありますが、ここでページの出力を行っています。

## ■占いサービスを組み立てる②
※実際の作業画面がスライドに載っています。参照してください

では、占いをするために実装を行います。

⑴ まず、ランダムで運勢を抽選するため、java.util.Randomをimportします。

```
import java.util.Random;
```
　
⑵ 運勢を管理するためのString型の配列を用意し、運勢を入れた状態で初期化します。

```
String luckList[] = {"大吉", "中吉", "吉", "半吉", "末小吉", "凶", "小凶", "半凶", "末凶", "凶", "大凶"};
```
　
⑶乱数を振るために、Randomクラスのインスタンスを生成し、nextIntで乱数を取得します。この際、運勢が入った配列の要素数を渡す事で、生成される乱数の範囲を限定しています。

```
Random rand = new Random();
//乱数所得
Integer index = rand.nextInt(luckList.length);
```
　
⑷あとは、運勢が入った配列の乱数番目に入っている要素を画面に表示するだけです。
　
完成したら、実行し、表示されたwebページのURLが下記の様になっているかを確認しましょう。

http://localhost:8080/プロジェクト名/FortuneTelling/

あなたの運勢は・・・？
