設問34

次のプログラムをコンパイルし、実行したときの結果として、正しいものを選べ（１つ）


```
import java.util.ArrayList;

public class Sample  {

 public static void main(String[] args){
 
  var list = new ArrayList<>();
  list.add("A");
  list.add(100);
  list.add("B");
  list.set(1,200);
  list.remove(2);
  list.set(3,300);
  
  System.out.println(list);
 
 }


}

```

A. [B, 300]が表示される


B. [A, 200, null, 300]が表示される


C. [A, 100, B]が表示される


D. 実行時に例外がスローされる



#ポイント

```
var list = new ArrayList<>();
list.add("A");   // index 0
list.add(100);   // index 1
list.add("B");   // index 2
list.set(1,200); // index 1 を 200 に置換 → OK
list.remove(2);  // index 2 ("B") を削除 → OK
list.set(3,300
```


#型推論
**var list = new ArrayList<>(); は「型推論を使って ArrayList の変数を宣言しているコード**  
Java 10 以降で使える ローカル変数型推論（var） の書き方。  


■コンパイラは右辺の型から変数の型を推論する。  

右辺：  
`new ArrayList<>();`  
これは ジェネリクス未指定の ArrayList（＝ raw 型）。  


■コンパイラ解釈：  

`ArrayList<Object> list = new ArrayList<>();`  
⇒list の型は ArrayList<Object> になる。  



■なぜ Object になるのか？
**ジェネリクスを指定しない new ArrayList<>(); は raw 型扱い**    

・要素型は Object  
・add するときは 何でも入る  

※ただし 型安全性の警告が出る  


という状態になる。