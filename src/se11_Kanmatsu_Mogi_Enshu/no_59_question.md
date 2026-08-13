設問59

次のコードの実行結果に関する説明として、正しいものを選べ（2つ）


□コード

```
List<Integer> list = List.of(5,4,3,2,1);
list.parallelStream().forEach(n -> System.out.print(n + " "));

```


A. forEachメソッドをforEachOrderedメソッドに置き換えると、「1 2 3 4 5」が出力される


B. 出力される数字の順番は毎回変わる


C. forEachメソッドをforEachOrderedメソッドに置き換えると、「5 4 3 2 1」のように出力されるが、順番は毎回変わる


D. forEachメソッドをforEachOrderedメソッドに置き換えると、「5 4 3 2 1」が出力される


E. 常に「5 4 3 2 1」が出力される



#ポイント
まず基本（↓）  
List.of(5,4,3,2,1) は 順序付きストリーム（ORDERED）   



**parallelStream + forEach → 順序は保証されない（毎回変わる）**
順序保証なし   
→ スレッドの実行順に依存  
→ 毎回変わる可能性がある  

**parallelStream + forEachOrdered → 元の順序（5→4→3→2→1）を保証する**  
 forEachOrdered は順序を固定する  
 毎回変わることはない。  
 
 