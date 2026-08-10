設問10


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


□コード1

```

public class Test implements AutoCloseable {

 @Override
 
public void close() throws Exception{
 
 throw new Exception("A");
}

}
```


□コード2

```
public static void main(String[] args){

 try(Test t = new Test()){
 
  throw new RuntimeException("B");
 }catch (Exception e) {
  System.out.println(e.getMessage());
 }
 }
}

```



A. 「A」と表示される


B. 「B」と表示される


C. 何も表示されない


D. Testクラスでコンパイルエラーとなる


E. Sampleクラスでコンパイルエラーとなる



#重要ポイント：try-with-resources の例外優先順位
Java の仕様：

・try 内で例外が発生  

・close() でも例外が発生  

**この場合 close() の例外が「主例外」になる、try 内の例外は 抑制例外（suppressed） になる。**  


つまり本コード例：  

主例外：Exception("A")  

抑制例外：RuntimeException("B")  

