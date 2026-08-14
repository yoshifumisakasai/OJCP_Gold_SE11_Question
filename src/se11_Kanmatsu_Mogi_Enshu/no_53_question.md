設問53

次のプログラムを確認してください。


□コード1

```

public class Order {

 private String name;
 private int price;
 
 public Order(String item, int price){
 
  super();
  this.item = item;
  this.price = price;
 }
 
 public String getItem(){
 
  return item;
 }

public int getPrice(){

 return price;
}
}

```


□コード2

```

List<Order> list = List.of(
new Order("apple", 100),
new Order("banana", 80));

BinaryOperator<Integer> op = (a, b) -> a + b;
int total = list.stream()
.map(o -> o.getPrice() * 10)
.reduce(0, op);

```

totalを導き出すコードと同じ結果になるものを選べ（１つ）


A. int result = list.stream()
   .mapToInt(o -> o.getPrice() * 10)
   .sum();
   
   
B. int result = list.stream()
   .map(Order::getPrice * 10)
   .reduce(op)
   .orElse(0);
   
   
C. int result = list.stream()
   .map(o -> o.getPrice() * 10)
   .reduce(op)
   .ifPresent(p -> p.intValue();
   
   
D. int result = list.stream()
   .mapToInt(o -> o.getPrice() * 10)
   .reduce(0, op);
   
   
#選択肢判定


B.

```
int result = list.stream()
    .map(Order::getPrice * 10)
    .reduce(op)
    .orElse(0);
```
    
❌ Order::getPrice * 10 は文法エラー
→ **メソッド参照に演算はできないため、コンパイルエラー**  

C.

```
int result = list.stream()
    .map(o -> o.getPrice() * 10)
    .reduce(op)
    .ifPresent(p -> p.intValue();
```

❌ **ifPresent は戻り値が voidであるため、int result = ... に代入できない**  
→ コンパイルエラー  
`void ifPresent(Consumer<? super T> action)`  
引数の Consumer は「値を受け取って処理する」だけで、値を返すことはできない　　
