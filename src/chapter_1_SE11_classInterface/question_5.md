設問5


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


```
public class Outer {

 void test(){
  Inner.message = "Hello, Java";
 }
 
 class Inner{
  private static String message;
  public void test(){
   System.out.println(message);
  }
 
 
 }
 
 public static void main(String[] args){
  Outer outer = new Outer();
  outer.test();
  outer.new Inner().test();
 
 }
}


```


A. 「null」と表示される

B. 「Hello, Java」と表示される

C. コンパイルエラーが発生する

D. 実行時に例外がスローされる



#ポイント
**コンパイルエラーが発生する理由は「非 static インナークラスに static フィールドを定義しているため」**  
**"static ネストクラスは OK / 非 static インナークラスは NG” のルール**  



#ポイント2

```
class Inner{
  private static String message;   // ★ここが NG
  public void test(){
    System.out.println(message);
  }
}
```
*Inner は 非 static インナークラス*  
→ static が付いていない  
→ Outer のインスタンスに紐づくインナークラス  

`非 static インナークラスは static フィールドを持てない`  

□Java の仕様：  
*非 static インナークラスは「Outer のインスタンスに属する」*
`インスタンスに属するクラスの中に static フィールドを置くことはできない`  
