設問43

商品リストから、商品の種類がいくつあるかを出力したい。プログラムに追加するコードとして、正しいものを選べ（１つ）


A. long count = list.stream()
                .filter(Item::getType)
                .distinct()
                .count();
                
                

B. long count = list.stream()
                .map(e -> e.getType)
                .collect(Collectors.toSet())
                .count();
                
                

C. long count = list.stream()
                .map(e -> e.getType())
                .count();
               

D. long count = list.stream()
                .map(Item::getType)
                .distinct()
                .count();
                
                
                
#選択肢判定

A. filter(Item::getType)
❌ コンパイルエラー

```
filter は Predicate<T> を要求する（戻り値 boolean）。
しかし Item::getType は Type を返すメソッド参照であり boolean ではない。
```



B. map(e -> e.getType).collect(Collectors.toSet()).count()
❌ コンパイルエラー

e.getType は メソッド呼び出しではなくフィールド参照扱い → コンパイルエラー

collect(Collectors.toSet()) の戻り値は Set<Type>

Set に count() は存在しない



#e.getType はメソッド呼び出しにならないのか？
**Java では メソッド呼び出しには必ず () が必要。**

```
e.getType() → メソッド呼び出し
e.getType → フィールドアクセス（＝変数参照）と解釈される
```

Java コンパイラ判断：

「getType という名前のフィールドが存在する」と推定する  
Item クラス：
`public Type getType() { ... }`  
という メソッドしかない。
フィールド getType は存在しないため コンパイルエラーになる。  
