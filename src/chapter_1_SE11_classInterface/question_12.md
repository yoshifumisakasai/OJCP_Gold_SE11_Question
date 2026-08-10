設問12


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


□コード1


```
public interface A {


 default void test(){
 
  System.out.println("A");
 }
}

```


□コード2

```

public class B {

 public void test() {
 
  System.out.println("B");
 }
}

```


□コード3

```
public class C extends B implements A {}

```


□コード4


```
public class Main{

 public static void main(String[] args){
  A a = new C();
  a.test();
 }
}

```


A. 「A」と表示される

B. 「B」と表示される

C. コンパイルエラーが発生する

D. 実行時に例外がスローされる




#Java のメソッド解決ルール
**クラスに同名メソッドがある場合、インタフェースの default メソッドは完全に無視される**  




#その他ポイント

```
A a = new C();  
a.test();  
```

ここで重要なのは：

**変数の型（A）ではなく、実体（new C()）でメソッドが決まる**  
**実体 C は B の test() を持っている**  





#ポイント

◆ 代入可否は is-a 関係だけで決まる   


**子 → 親：OK**  

**親 → 子：NG**  

**実装クラス → インタフェース：OK**    

**インタフェース → 実装クラス：NG**    