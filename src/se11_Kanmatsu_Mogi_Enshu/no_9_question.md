設問9


次のインタフェースのうち、戻り値を戻さないメソッドを持つものを選べ（１つ）


A. java.util.function.Predicate


B. java.util.function.Function


C. java.util.function.Supplier


D. java.util.function.Consumer


#各インタフェースの戻り値

A. Predicate  
`boolean test(T t)`    
引数あり  
戻り値：boolean（戻す）    
❌ 戻り値を戻さないインタフェースではない  


B. Function  
`R apply(T t)`   
引数あり  
戻り値：R（戻す）    
❌ 戻り値を戻す


C. Supplier 
`T get()`  
引数なし  
戻り値：T（戻す）    
❌ 戻り値を戻す



D. Consumer（正解）  
`void accept(T t)`  
引数あり
戻り値：void（戻さない）  
⭕ 条件に完全一致


