設問7

非推奨のメソッドの使用時に出力される警告を抑制（オフ）するために指定するアノテーションの記述として、正しいものを選べ（１つ）


A. SuppressWarnings


B. SuppressWarnings("unchecked")


C. SuppressWarnings("removal")


D. SuppressWarnings("deprecation")


#ポイント

**非推奨（@Deprecated）のメソッドを呼び出したときに出る 「deprecation 警告」 を抑制するには、@SuppressWarnings("deprecation") を指定します。**  



〇典型的な使い方  

```
@SuppressWarnings("deprecation")
public void useOldMethod() {
    oldMethod(); // Deprecated
}
```

`SuppressWarnings`  
→ 引数なしは 無効。何の警告を抑制するか指定していないため誤り。  

`SuppressWarnings("unchecked")`    
→ 未チェックキャスト（ジェネリクス）に関する警告を抑制するもの。非推奨警告とは無関係  


`SuppressWarnings("removal")`    
→ Java 9 以降で導入された「削除予定 API」への警告を抑制するもの。  
@Deprecated(forRemoval=true) のケース。今回の「非推奨メソッドの使用警告」とは別。  

