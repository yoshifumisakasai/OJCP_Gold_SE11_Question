設問6


Comparatorの実装として、正しいものを選べ（１つ）



A. public class A implements Comparator {

    @Overide
    public boolean compare(Object o1, Object o2) {
    
     return o1.equals(o2);
    }
   }
   
B. public class A implements Comparator {

    @Overide
    public boolean compare(String str1, String str2) {
    
     return str1.length() - str2.length();
    }
   }
   
C. new Comparator<String>() {

    @Overide
    public int compare(String o1, String o2) {
    
     return o1.compareTo(o2);
    }
   }
   
   
D. new Comparator<String>() {

    @Overide
    public int compareTo(String o1, String o2) {
    
     return o1.compareTo(o2);
    }
   }
   
   


#インタフェースComparator<T>  
Comparator が実装すべきメソッドは compare(T o1, T o2)（戻り値 int）


#compareTo はどこに属する？

Comparable<T> インタフェースの抽象メソッド  


```
public interface Comparable<T> {
    int compareTo(T o);
}
```
・compareTo は Comparable の持ち物  
・実装クラス（String, Integer, LocalDate など）が override して使う  

※String が Comparable<String> を実装しているため。  
