設問19

次のプログラムをコンパイル、実行したときの結果として、正しく記述されているものを選べ（１つ）

```
import java.util.HashSet;
import java.util.LinkedList;
import java.util.List;
import java.util.Set;


public class Sample{

 public static void main(String[] args){
 
  List<String list = new LinkedList<>();
  Set<String> set = new HashSet<>();
  String[] array = {"a", "b", "c", "d", "e"};
  for(String str : array){
  
   list.add(str);
   set.add(str);
  
  }
  
  System.out.print(set.size()+ "," + list.size() + ",");
  Set set2 = new HashSet<>(list);
  List list2 = new LinkedList<>(set);
  System.out.print(set.size() + "," + list2.size());
  
 }
}
```

A. 「5,5,4,4」と表示される


B. 「4,5,4,4」と表示される


C. 「4,5,4,5」と表示される


D. 「4,4,4,4」と表示される



#List と Set の性質（重複可・重複不可）

■list（LinkedList）  
`list.add(str);`  
→ 重複を許す   

■set（HashSet）  
`set.add(str);`  
→ 重複を許さない  
