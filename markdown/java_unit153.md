# 標準クラス
## 文字列編

## ■文字の操作
システム上のデータは、多くが数値や文字として扱われます。そのため、文字操作の関数は多く存在します。

ここでは、良く使う文字操作関数を幾つかご紹介します。

**文字の長さを調べる（lengthメソッド）：**
  * **◆文字の文字数を調べる**  
　　変数 = String変数.length();  
　　※文字コードは省略可能

```
// Javaクラスファイル内
class Sample {
    public static void main(String[] args) {
        String word = "文字列操作の勉強！";

        // 文字列の長さを表示 -- 9
        System.out.println(word.length());
    }
}
```

**部分的に文字を取得（substringメソッド）：**
  * **部分的に文字を取得（以降全部）**  
　　変数 = String変数.substring(開始位置);  
  * **部分的に文字を取得（指定文字数）**  
　　変数 = String変数.substring(開始位置, 終了位置);  

開始位置も終了位置も、0がスタート。

```
// Javaクラスファイル内
class Sample {
    public static void main(String[] args) {
        String word = "文字列操作の勉強！";

        // 5番目以降を取得 -- "作の勉強！"
        System.out.print(word.substring(4));

        // 3番目から6番目まで取得 -- "列操作"
        System.out.print(word.substring(2, 5));
    }
}
```

**文字の空白除去（trimメソッド）：**  
  * **文字の前後の空白を取り除く**  
　　変数 = String変数.trim();

**文字の比較（equalsメソッド）：**  
  * **文字を比較し、一緒ならtrue、違えばfalse**  
　　変数 = String変数.equals(比較文字列);

```
// Javaクラスファイル内
class Sample {
    public static void main(String[] args) {
        String word = "    あいうえ ";

        // 空白を除去 -- "あいうえ"
        System.out.print(word.trim());

        // wordと"たまご"を比較 -- "false"
        System.out.print(word.equals("たまご"));
    }
}
```  

**文字が含まれる位置を取得（indexOfメソッド）：**
  * **指定文字の位置を取得**  
　　変数 = String変数.indexOf(指定文字);

**文字の置換（replaceメソッド）：**
  * **指定文字を別の文字へ置き換え**  
　　変数 = String変数.replace(検索文字, 置換文字);

```
// Javaクラスファイル内
class Sample {
    public static void main(String[] args) {
        String word = "きょうははれです。";

        // 文字位置の取得 -- "ははれ"が見つかるのは3番目
        System.out.print(word.indexOf("ははれ"));

        // 文字の置換 -- "はれ"を"あめ"に
        System.out.print(word.replace("はれ", "あめ"));
    }
}
```
## ■文字と配列
プログラム上で扱う文字の中には、特定の文字を区切りとして複数の情報を保持している場合があります。有名なものでは **CSV（Comma Separated Value）** と呼ばれる形式があります。

「,」を区切りとして、複数の情報を連結したテキスト情報を **CSV** と呼びます。

この様な形式の情報を扱うのに適したメソッドも用意されています。

**特定の文字で区切って配列化（splitメソッド）：**    
　　変数 = String変数.split("");

```
// Javaクラスファイル内
class Sample {
    public static void main(String[] args) {
        String word = "ケーキ,クッキー,アイス";

        // 文字の配列化 -- お菓子が配列化
        String[] sweets = word.split(",", 0);
    }
}

```
