設問63


次のうち、プリミティブ型のデータを戻すことができるインタフェースを選べ（１つ）


A. java.util.function.ToDoubleFunction


B. java.util.function.Supplier


C. java.util.function.LongConsumer


D. java.util.function.BiFunction




------------------------------------


■選択肢判定

`ToDoubleFunction<T>`  
抽象メソッド：double applyAsDouble(T value)  

戻り値が double（プリミティブ）  

✔ プリミティブ型を返す → 正解  



`Supplier<T>`  
抽象メソッド：T get()  

戻り値は T（参照型）  

プリミティブを返すには Supplier<Integer> のようにラッパー型になる  
→ プリミティブは返せない  



`LongConsumer`  
抽象メソッド：void accept(long value)  

引数は long（プリミティブ）だが、戻り値は void  

→ 戻り値なし  



`BiFunction<T, U, R>`  
抽象メソッド：R apply(T t, U u)  

戻り値は R（参照型）  

プリミティブは返せない  