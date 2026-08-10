設問5

appleの価格の平均を求めたい。次のプログラムの「insert code here」に入るコードとして、正しいものを選べ（１つ）


```
import java.util.List;
import java.util.stream.Collectors;


public class Sample {

 List<Item> list = List.of(
 new Item("apple", 100),
 new Item("banana", 80),
 new Item("apple", 200)
 );
 //insert code here
 
 System.out.println(result);

 }
}
```


A. double result = list.stream()
   .filter(e -> e.getName().equals("apple"))
   .mapToInt(Item::getPrice)
   .average()
   .getAsDouble();
   
   
B. double result = list.stream()
   .filter(e -> e.getName().equals("apple"))
   .average()
   .getAsDouble();
   
   
C. double result = list.stream()
   .filter(e -> e.getName().equals("apple"))
   .filter(s -> s.getPrice())
   .average()
   .getAsDouble();
   
   
D. double result = list.stream()
   .collect(Collectors.groupingBy(Item::getName,
   Collectors.averagingDouble(Item::getPrice)));
   


#ポイント   
**average() は IntStream / DoubleStream / LongStream にしか存在しない**  

**filter の条件は boolean が必要**  




■Collectors.groupingBy の戻り値は Collector<T, ?, Map<K, V>>。  
collect の戻り値は Map<K, V> になる。  

```
double result = list.stream()
   .collect(Collectors.groupingBy(Item::getName,
   Collectors.averagingDouble(Item::getPrice)));
```
上記例では、groupingBy で Map<String, Double> が返る  
result は double で宣言されている→ 型不一致でコンパイルエラー  


〇正しいコード：  

```
Map<String, Double> map =
    list.stream()
        .collect(Collectors.groupingBy(
            Item::getName,
            Collectors.averagingDouble(Item::getPrice)
        ));

double result = map.get("apple");
```


#Java の仕様的な観点とSQL 的な観点  
Collectors.groupingBy(Item::getName, Collectors.averagingDouble(Item::getPrice)) は
SQL の GROUP BY name に AVG(price) を組み合わせた処理とほぼ同じ構造で動く。  

□Java Stream の groupingBy は「SQL の GROUP BY を Java のオブジェクト世界で再現したもの」と理解する  



(Java の仕様的な観点とSQL 的な観点の両方か)  


■groupingBy の型構造
`Collector<T, ?, Map<K, R>>`  
T：ストリームの要素（Item）  
K：グループ化キー（Item::getName → "apple", "banana"）  
R：グループごとの最終結果（averagingDouble → Double）  

つまり groupingBy は：
「ストリームを走査し、キー K ごとに要素を集め、
そのグループに対して downstream Collector を適用して R を作る」
という Collector。  

■groupingBy の処理フロー（Java の内部動作）  
ストリームを 1 要素ずつ処理しながら、内部で Map<K, A> を構築する。  
1.要素を 1 つ取り出す  

2.分類キー K を計算する  
  Item::getName → "apple" など

3.Map に K が存在するか確認
なければ新しいグループを作る

4.downstream Collector（averagingDouble）に値を渡す
  ※averagingDouble は内部で「合計」「件数」を保持する

5.最終的に Map<K, R> を返す
R は averagingDouble によって計算された平均値

つまり groupingBy は Map を使ったグループ化処理であり、
downstream Collector が「グループごとの集計方法」を決める。


🍎 SQL の GROUP BY と完全に対応づけるとこうなる

```
SELECT name, AVG(price)
FROM items
GROUP BY name;
```

