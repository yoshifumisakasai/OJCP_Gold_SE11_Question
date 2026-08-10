設問48

次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


□コード1

```
public class Item {

 private String name;
 private int price;
 
 public Item(String name, int price){
 
  super();
  this.name = name;
  this.price = price;
 }
 
 public String getName(){
 
  return name;
 }
 
 public int getPrice(){
 
  return price;
 }

}

```





□コード2

```

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class Sample {

 public static void main(String[] args) {
 
  List<Item> list = new ArrayList<>(List.of(
  new Item("banana", 100),
  new Item("apple", 80),
  new Item("orange", 80)));
  
  list.sort(
  Comparator.comparing(Item::getPrice)
  .thenComparing(Item::getName)
  .reversed());
  
  list.forEach(item ->
  System.out.print(" " + item.getName()));
 }
}
```

A. [banana orange apple]と表示される

B. [apple orange banana]と表示される

C. [apple banana orange]と表示される

D. [banana apple orange]と表示される


#「Comparator の評価順序 → reversed の作用  

② Comparator.comparing(Item::getPrice)
まず price 昇順で比較する。

昇順：

apple (80)

orange (80)

banana (100)
 

                                     

③ thenComparing(Item::getName)
price が同じ場合は name 昇順（辞書順）で比較。

80 円組は：

apple

orange

辞書順では apple < orange なのでこの順で確定。



④ reversed()
ここがポイント。

Comparator 全体を反転する  
→ 並び順を丸ごと逆にする。



`static <T,U extends Comparable<? super U>> Comparator<T> comparing(Function<? super T,? extends U> keyExtractor)`




#comparing の Java API 仕様（自然順序版）

`static <T,U extends Comparable<? super U>> Comparator<T> comparing(Function<? super T,? extends U> keyExtractor)`

● 型パラメータの意味
T：比較対象の型（今回なら Item）

U：比較キーの型
しかも U extends Comparable<? super U>  
→ U は Comparable を実装している必要がある
→ つまり 自然順序で比較できる型（Integer, String など）


□keyExtractor の役割
`Function<? super T, ? extends U>`    
→ T（Item）から U（price の int → Integer）を取り出す関数


□comparing の動作
keyExtractor.apply(item) でキーを取り出す

そのキー同士を 自然順序（Comparable.compareTo） で比較する Comparator を返す

つまり comparing(Item::getPrice) は：

Item を受け取り、price をキーとして昇順比較する Comparator を作る





#「Comparator.comparing(Item::getPrice)」が実際に何をしているか
● Item::getPrice の型
int getPrice()  
→ comparing の keyExtractor は Integer に自動ボックス化される
→ Integer は Comparable を実装している
→ comparing の「自然順序版」が使われる



● 内部で生成される Comparator のイメージ
Java の comparing の内部はほぼこう：

```
return (a, b) -> {
    U keyA = keyExtractor.apply(a);
    U keyB = keyExtractor.apply(b);
    return keyA.compareTo(keyB);  // 自然順序
};
```
comparing(Item::getPrice) は：

`(a, b) -> Integer.compare(a.getPrice(), b.getPrice())`  
と同じ意味。