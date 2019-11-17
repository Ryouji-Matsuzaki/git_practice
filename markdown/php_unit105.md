## 総まとめ
### YahooショッピングAPIについて

### ■YahooショッピングAPIの利用

1. **[http://developer.yahoo.co.jp/](http://developer.yahoo.co.jp/)**にアクセスして、デベロッパーアカウントを取得(yahooIDを取得している必要あり)

2. 「デベロッパーネットワークトップ > アプリケーションの管理 > 新しいアプリケーションを開発」とアクセスし、アプリケーションの種類に「サーバーサイド」を選択。他は適当に入力しても構わない。規約に同意し、続行。アプリケーションIDが入手できます(以後いつでも確認できる)。

3. ショッピング検索APIについては**[こちら](https://developer.yahoo.co.jp/sample/shopping/sample1.html)**を参照してください。
サンプルコードはほぼそのまま使用できます。

&nbsp;

### ■YahooショッピングAPIで取得できるデータ

今回利用するYahooショッピングAPIの様に、情報を渡すと特定の処理をしてくれる、インターネットに公開されている機能をWebAPIと呼びます。

WebAPIでは、処理結果を特定のフォーマットで返却してくれます。
利用者はフォーマットされたデータを解析し、処理結果を取得します。

フォーマットとして良く利用されるのは、xmlとjsonと呼ばれる形式です。

&nbsp;

### ■YahooショッピングAPIのポイント

YahooショッピングAPIの情報が下記にまとめられています。利用しましょう。

**[YahooショッピングAPI - デベロッパーネットワーク](https://developer.yahoo.co.jp/webapi/shopping/)**

また、商品情報の取得で困ったら、下記も見てみましょう。

**[商品検索](https://developer.yahoo.co.jp/webapi/shopping/shopping/v1/itemlookup.html)**

responsegroupの指定で、取れる情報と取れない情報があります。
