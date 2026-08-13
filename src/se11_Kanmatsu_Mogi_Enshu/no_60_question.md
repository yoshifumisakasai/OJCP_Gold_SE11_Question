設問60

次のプログラムは実行すると例外が発生する。例外の発生を解消する方法として、正しいものを選べ（１つ）

```

import java.util.Arrays;

public class Sample {

 static classItem {
 
  private String name;
  public Item(String name){
  
   super();
   this.name = name;
  }
 }


public static void main(String[] args){

 Item[] items = {
 
  new Item("apple"),
  new Item("orange"),
  new Item("banana")
 };
 
 Arrays.sort(items);
 for(Item item : items){
 
  System.out.println(item.name);
 }
}
}

```


A. ItemクラスがComparator<Item>を実現するようにし、次のコードを実装する
   public int compare(Item a, Item b){
    return a.name.compareTo(b.name);
   }



B. ItemクラスがComparator<Item>を実現するようにし、次のコードを実装する
   public int compareTo(Item o){
    return name.compareTo(o.name);
   }
   
   
 
C. ItemクラスがComparable<Item>を実現するようにし、次のコードを実装する
   public int compare(Item a, Item b){
    return a.name.compareTo(b.name);
   }
   
   
      
D. ItemクラスがComparable<Item>を実現するようにし、次のコードを実装する
   public int compareTo(Item o){
    return name.compareTo(o.name);
   }




#インタフェースComparator<T>
@FunctionalInterface  
public interface Comparator<T>  

型パラメータ:
T - このコンパレータにより比較されるオブジェクトの型


int compare(T o1, T o2)  
順序付けのために2つの引数を比較します。 最初の引数が2番目の引数より小さい場合は負の整数、両方が等しい場合は0、最初の引数が2番目の引数より大きい場合は正の整数を返します。  


#インタフェースComparable<T>
public interface Comparable<T>  
型パラメータ:  
T - このオブジェクトが比較されるオブジェクトの型  

int compareTo(T o)  
このオブジェクトと指定されたオブジェクトの順序を比較します。 このオブジェクトが指定されたオブジェクトより小さい場合は負の整数、等しい場合はゼロ、大きい場合は正の整数を返します。  



#ポイント

```
   public int compare(Item a, Item b){
    return a.name.compareTo(b.name);
   }
```

Comparator<Item> を実装し、compare を定義する  
→ Arrays.sort(items) は Comparator を使いません  
→ Comparator を使うなら Arrays.sort(items, new Item()) のように Comparator を渡す必要ある  


`public class Arrays extends Object`  

static <T> void	sort(T[] a, Comparator<? super T> c)	
指定されたコンパレータが示す順序に従って、指定されたオブジェクトの配列をソートします。  


■型パラメータ:  
T - ソートされるオブジェクトのクラス   
〇パラメータ:  
a - ソートされる配列  
c - 配列の順序を決定するコンパレータ。 null値は、要素の自然順序付けが使用されることを示す。  

