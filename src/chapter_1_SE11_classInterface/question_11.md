設問11

次のプログラムの、「insert code here」に記述するコードとして、正しいものを選べ（１つ）



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
public interface B {

 default void test() {
 
  System.out.println("B");
 }
}

```




□コード3


```
public interface C extends B {}


```


□コード4

```
public interface D extends C {}


```



□コード5


```
public class Sample implements A, D {


 @Override
 public void test() {
 
  // insert code here
 }
}


```



A. A.super.test();


B. B.super.test();


C. C.super.test();


D. 上記の選択肢はいずれもコンパイルエラーが発生する




#Java のルール（重要）
複数のインタフェースから同名 default メソッドが来た場合：  

**どのインタフェースのメソッドを使うか明示しなければならない。その際に使えるのは「直接実装しているインタフェース」だけ**  

