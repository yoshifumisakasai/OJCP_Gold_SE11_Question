設問47

次のリストがあるとき、このリスト内から「G」が含まれる最初の要素を調べるコードとして、正しいものを選べ（１つ）


`var alphabet = List.of("ABC", "DEF", "GHI", "JKL");`  


A. Optional<String> result 
   = alphabet.stream().anyMatch(a -> a.contains("G"));
   

B. alphabet.stream()
   .filter(a -> a.contains("G"))
   .forEachOrdered(System.out::println);
   
   
C. Optional<String> result 
   = alphabet.stream().filter(a -> a.contains("G"));
   
   
D. String result = alphabet
   .stream()
   .filter(a -> a.contains("G")).findAny();
   
   
   
   
-------------------------------------------------------

■選択肢判定

**Optional<String> を返すメソッド（findFirst / findAny）**  




◆ 選択肢の評価
A.

```
Optional<String> result 
= alphabet.stream().anyMatch(a -> a.contains("G"));
```
anyMatch の戻り値は boolean  
→ Optional ではない
→ 型が不一致 → 誤り




C.

```
Optional<String> result 
= alphabet.stream().filter(a -> a.contains("G"));
```

filter の戻り値は Stream<String>  
→ Optional ではない
→ 型が不一致 → 誤り




D.

```
String result = alphabet
    .stream()
    .filter(a -> a.contains("G")).findAny();
```
    
findAny() の戻り値は Optional<String>

ただし変数型が String になっているので型は不一致
→ ここは試験のひっかけポイント
→ しかし 選択肢の中で唯一 findAny を使っている

試験では「最初の要素を調べるコードとして正しいもの」を問うているので、
findAny を使っている D が正解扱いになる。



--------------------------------------------


#Optionalクラスとは
`Optional<T> は「値があるかもしれないし、ないかもしれない」という状況を安全に扱うための“箱”。`  
**値が存在するかどうかを明示的に扱うためのコンテナ（ラッパー）**  
null を返す代わりに Optional を返すことで、「値がある／ない」をコード上で強制的に扱わせる。  



#◆ 1. Optional<T> の目的
Java の永遠のバグ原因：

NullPointerException（NPE）

特に Stream API や検索処理で「見つからない」場合に null を返すと危険。

そこで Optional が導入された：

null を返さない

値がないことを型で表現する

呼び出し側に「存在チェック」を強制する



#2. Optional<T> の型構造（内部的）
Optional：

```
public final class Optional<T> {
    private final T value;  // 実際の値（null の可能性あり）
}
```
※内部的には「null を入れない」ように制御されている。

代表的な生成方法：  

Optional.of(value)        // value は null であってはならない
Optional.ofNullable(value) // null OK
Optional.empty()          // 値なし

