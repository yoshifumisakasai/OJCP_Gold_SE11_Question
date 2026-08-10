設問7

次のプログラムをコンパイル、実行した結果として正しいものを選べ（１つ）


□コード1

```
public class A implements AutoCloseable {

 @Override
 public void close() throws Exception {
 
  System.out.println("A");
 }

}
```


□コード2

```
public class B implements AutoCloseable {

 @Override
 public void close() throws Exception {
 
  System.out.println("B");
 }

}


```


□コード3

```
public class C implements AutoCloseable {

 @Override
 public void close() throws Exception {
 
  System.out.println("C");
 }

}


```

□コード4

```
public class TestUsing {

 public static void main(String[] args) throws Exception {
 
  A a = new A();
  try (a;
       B b = new B();
       C c = new C()){
       
        // do something
       }
 
 }


}

```


A. 「A」、「B」、「C」と表示される

B. 「B」、「C」、「A」と表示される

C. 「C」、「B」、「A」と表示される

D. 「A」、「C」、「B」と表示される



#ポイント

try-with-resources の close() は「最後に宣言したリソースから順に」呼ばれる。　　
つまり 逆順で close が実行される。　　


□Java の try-with-resources は内部的に次のような構造：

```
try {
    // do something
} finally {
    c.close();
    b.close();
    a.close();
}
```
**スタック構造（LIFO）でリソースを閉じる**
**後から開いたリソースは先に閉じる必要がある（例：入れ子のストリームなど）**  
