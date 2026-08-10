設問17

次のプログラムはコンパイルエラーとなる。コンパイルエラーの解決方法として、正しいものを選べ（2つ）


```
import java.util.List;
import java.util.Optional;

public class Sample {

 public static void main(String[] args){
  
  List<Item> items = List.of(
  new Item("A", 100),
  new Item("B", 200),
  new Item("C", 300)
  );
  
  Stream itemStream = items.stream();
  itemStream.filter(item -> item.getPrice() > 200)
  .forEach(System.outn::println);
 }

}

```


A. itemsStreamのfilterメソッドに渡す引数を、「item -> (Item) item).getPrice() > 200」に置き換える


B. itemStreamのfilterメソッドに渡す引数を、「(Item item) -> item.getPrice() > 200」に置き換える


C. 変数itemStreamのデータ型をStreamからStream<Item>に置き換える


D. List<Item> itemsを初期化すうるために、「List.stream();」の結果を代入する




# ジェネリクスとラムダ式の型推論
**「itemStream が raw 型（型パラメータなし）なのでラムダ式の item が Object と推論され、getPrice() が呼べずコンパイルエラーになる」。**  


```
Stream itemStream = items.stream();
itemStream.filter(item -> item.getPrice() > 200)
         .forEach(System.out::println);
```

（itemStream が raw 型（Stream）型パラメータがないため、item の型は Object と推論）  



#正しい修正方法は2つ

■変数 itemStream の型を Stream<Item> にする  
`Stream<Item> itemStream = items.stream();`  
これでラムダ式の item が Item と推論されるため、item.getPrice() が呼べる。  


■filter のラムダ式で型を明示する  
`itemStream.filter((Item item) -> item.getPrice() > 200)`   
ラムダ式の引数に型を明示すると、raw 型の Stream でもコンパイルが通る。  
