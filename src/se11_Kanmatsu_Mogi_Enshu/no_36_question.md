設問36

次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）

```
import java.util.ArrayList;
import java.util.List;

public class Sample {

 public static void main(String[] args){
 
  List<Integer> a = new ArrayList<>();
  a.add(1);
  a.add(2);
  
  List b = List.copyOf(a);
  b.add(3);
  
  List<List<Integer>> c = List.of(a,b);
  System.out.println(c);
 }

}

```

A. [[1,2,3],[1,2,3,]]が表示される


B. [[1,2],[1,2]]が表示される


C. [[1,2],[1,2,3]]が表示される


D. コンパイルエラーが発生する


E. 実行時に例外がスローされる



#実行時の例外スロー

今回のポイントは 
**List.copyOf が返すリストは「不変（immutable）」であるという仕様。**  
そのため、b.add(3) の時点で *「UnsupportedOperationException」* が必ず発生する。


Java Gold 対策として、内部仕様、流れを整理。

〇コードの実行  

```
List<Integer> a = new ArrayList<>();
a.add(1);
a.add(2);
```
ここまでで a = [1, 2]。



■List.copyOf(a) の仕様  

`List b = List.copyOf(a);`
**List.copyOf は Java 10 以降の不変コレクション API。**  

**返すリストは java.util.ImmutableCollections.ListN**  

※add/remove/set などの変更操作は 「UnsupportedOperationException」  

つまり：
b.add(3);  // ← ここで例外  
📌 例外の種類
`java.lang.UnsupportedOperationException`  
これは 実行時例外。  
