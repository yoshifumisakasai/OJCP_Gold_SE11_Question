設問9

次のプログラムの説明として、正しいものを選べ（１つ）


□コード1

```
public interface A {

 static void test() {
 
  System.out.println("A");
 }
}

```


□コード2

```
public interface B extends A {}

```



□コード3

```
public class C implements A {}

```



□コード4

```

public class D implements A {

 public static void main(String[] args){
 
  A.test();
  B.test();
  C.test();
  test();
 }

}
```


A. Dクラスの3行目でコンパイルエラーが発生する

B. Dクラスの４行目でコンパイルエラーが発生する


C. Dクラスの5行目でコンパイルエラーが発生する

D. Dクラスの6行目でコンパイルエラーが発生する




#解法


■各行の意味とコンパイル可否

1️⃣ A.test();
test() は A インタフェースの static メソッド

`static メソッドは 宣言したインタフェース名でのみ呼び出せる`      
➡ コンパイル OK



2️⃣ B.test();
B は A を extends しているが

`static メソッドは継承されない（インスタンスメソッドとは扱いが違う）`    

よって B には test() が存在しない
➡ コンパイルエラー（ここが最初のエラー）



3️⃣ C.test();
C は A を implements しているが

`static メソッドは実装クラスに継承されない`      
➡ コンパイルエラー（ただし B.test() の方が先にエラーになる）



4️⃣ test();
クラス D に test() は存在しない

`static メソッドは インタフェース名を付けて呼び出す必要がある`      
➡ コンパイルエラー（ただし B.test() の方が先にエラーになる）