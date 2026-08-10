設問2


次のプログラムの「insert code here」に記述するコードとして、正しいものを選べ（１つ）


```
public class Outer {
 class Inner {
  public void test(){
  
   System.out.println("test");
  }
 }
 
 public static void main(String[] args){
  //insert code here
 }
}



```




A. new Inner();

B. new Outer.Inner();


C. new Outer().new Inner();


D. new Outer:Inner();



#ポイント1
**非 static インナークラスは Outer インスタンスに紐づいている。つまり、Outer のインスタンスなしでは生成できない**  


#ポイント2
✔ static メソッドには「this」が存在しない
**Java の static メソッドは クラスに属するメソッド であり、インスタンスに属していない**  

`インスタンスメソッド → this がある`  
`static メソッド → this がない`  

#ポイント3

**非 static インナークラスは「Outer の this が必須」**
*非 static インナークラスは、Java の内部的にはこういう構造になっている：*  

```
class Inner {
    Inner(Outer this$0) { ... }
}
```
※Inner を new するには Outer のインスタンス（this）が必ず必要  
※main の中で new Inner() ができない理由は、渡すべき Outer のインスタンス（this$0）が存在しないためで、コンパイルエラー  
