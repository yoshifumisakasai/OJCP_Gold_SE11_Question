設問66


次のコードのうち、正しく記述されているものを選べ（１つ）



A. Function func = String::toUpperCase;


B. UnaryOperator<String> func = String::toUpperCase;


C. Function<String> func = s -> s.toUpperCase();


D. UnaryOperator func = s -> s.toUpperCase();


-------------------

#選択肢判定


A. `Function func = String::toUpperCase;`  
*Function は 原型（raw type） を使っており、型パラメータがない*  

**Function<T,R> の T と R を指定していないため不正***  
**Raw type はコンパイル警告ではなく、このケースでは型不一致でコンパイルエラー**  



B. `UnaryOperator<String> func = String::toUpperCase;`  
**UnaryOperator<T> は Function<T,T> の特殊化**

〇「String::toUpperCase」  
引数：String  
戻り値：String   
→ UnaryOperator<String> と完全一致  



C. `Function<String> func = s -> s.toUpperCase();`  
Function<String> は 型パラメータが1つしかないため不正    
**Function<String, String> のように 2つ必要**  



D. `UnaryOperator func = s -> s.toUpperCase();`  
Raw type（型パラメータなし）なので 不正  

**UnaryOperator<String> と書く必要あり**  
