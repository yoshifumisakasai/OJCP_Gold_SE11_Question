設問13


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


□コード1


```
public interface A {
 
 public default void test() {
 
  System.out.println("A");
 }
}


```


□コード2


```
public abstract class B {

 protected void test() {
 
  System.out.println("B");
 
 }
}

```



□コード3


```

public class Sample extends B implements A {


 public static void main(String[] args){
 
  new Sample().test();
 }
}

```


A. 「A」と表示される


B. 「B」と表示される


C. コンパイルエラーが発生する

D. 実行時に例外がスローされる



#ポイント1
**アクセス修飾子は protected**  

1. 同一クラス内  
（当然 OK）  

2. 同一パッケージ内  
（package-private と同じ範囲）   

3. サブクラス（継承したクラス）からアクセス可能  



#ポイント2
**クラスに同名メソッドが存在する場合、インタフェースの default メソッドは完全に無視される**
