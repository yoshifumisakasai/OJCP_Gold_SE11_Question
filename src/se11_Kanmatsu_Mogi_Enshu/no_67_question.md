設問67


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


□コード1


```
public class Test<T> {

 public int count(T[] array, T val){
 
  int count = 0;
  for(T v : array){
  
   if(val.equals(v)){
   
    count++;
   }
  
  }
  return count;
 }

}

```




□コード2


```
public class Sample {

 public static void main(String[] args){
 
  String[] array = {"A", "B", "C", "D"};
  Integer[] array2 = {1,2,3,4,5};
  
  Test test = new Test();
  Test<String> test2 = new Test<>();
  
  System.out.println(test2.count(array, "A"));
  System.out.println(test.count(array, "A"));
  System.out.println(test.count(array2, 1));
  
 }

}


```


A. 「1」「null」「null」の順に表示される


B. 「1」「1」「1」と表示される


C. コンパイルエラーとなる。


D. 実行時にNullPointerExceptionがスローされる


E. 実行時にClassCastExceptionがスローされる


#ポイント1

**Test を raw type（Test test = new Test();） として使った行で、**  
**型パラメータが消滅し、Object[] として扱われるため、内部で不正なキャストが発生する。**  



`Test の型パラメータ T は 消滅`  

`コンパイル時には T が Object として扱われる`  

*しかし内部の val.equals(v) の部分で 実際には T として扱おうとしてキャストが入る*  
Java のジェネリクスは 型消去（type erasure） により、内部的には次のようなキャストが入る：
(Java の型消去（type erasure）によって、コンパイル時に暗黙のキャストが自動挿入されるという意味)  

`T v = (T) array[i];`  
raw type の場合、このキャストが 実行時に危険。  



#ポイント2

test.count(array2, 1)
ここで破綻する。

array2 は Integer[]  
raw type のため、内部で Integer を T（＝Object）として扱うが、equals の呼び出しでキャストが入る  
実際には val.equals(v) の評価時にInteger を String として扱おうとするキャストが発生する  

つまり：
`String.equals(Integer)`  
ではなく、

内部的に
`(T) v   // v は Integer`  
が起こり、Integer を String にキャストしようとして ClassCastException

その結果、  
test.count(array2, 1) の実行時に ClassCastException が発生する。  