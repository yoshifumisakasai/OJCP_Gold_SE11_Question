設問54

次のコードのうち、正しく記述されているものを選べ（１つ）


A. Consumer a = msg -> System.out::println;


B. Consumer b = (String msg) -> System.out.print(msg);


C. Consumer c = System.out::print;


D. Consumer d = var msg -> {System.out.println(msg);};


#ポイント

Consumer は 引数を1つ取り、戻り値なし（void）で処理する関数型インターフェース。  
抽象メソッドは void accept(T t)。  


---------------------------------------------
■(選択肢判定）


・選択肢A
❌ System.out::println は メソッド参照    
→ msg -> System.out::println は「msg を受け取って println メソッド参照を返す」形になる  
→ Consumer は 戻り値なしなので不適合  



・選択肢D
❌ **var はラムダの引数型に使えない**  
→ var msg -> ... は Java では禁止



・選択肢C
C. Consumer c = System.out::print;
❌ 一見正しそうだが 型推論が成立しない

System.out::print はオーバーロード多数:  

・print(String)
・print(int)
・print(char)
など複数あるため、**Consumer に型推論できない**  

  
→ Consumer<String> c = System.out::print; と書けば OK
→ しかし問題文は **型パラメータなしの raw Consumer → コンパイルエラー**  