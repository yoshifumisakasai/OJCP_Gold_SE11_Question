設問3


次のTestインタフェースを実装したサービスをロードするために、ServiceLoader<Test>型のサービスローダーloaderを作成した場合、Testのexecute()メソッドを呼び出すには、どのコードを実行すればよいか、正しいものを選べ（１つ）



```
public interface Test {

 public void execute();
}

```


A. for ( Test test : loader ){

    test.execute();

   }
   
   
   
B. loader.exexute();


C. for ( Test test : loader.services()) ){

    test.execute();

   } 
   


D. Test test = loader.getTest();

   test.execute();




#ポイント

■(解説1)    
ServiceLoader でロードしたサービスのメソッドを呼び出すには、  
ServiceLoader<Test> は Iterable<Test> を返すので、for-each で取り出して execute() を呼ぶのが正しい。  


■(解説2)  
ServiceLoader は Iterable<Test> を実装しているため、
loader を for-each で回すと ロードされたサービス実装が順に取得できる。
その test に対して execute() を呼べばよい。




#ServiceLoader
 ServiceLoader は「サービス実装を動的に発見してロードするための仕組み（SPI：Service Provider Interface）」です。  
Java 標準が提供する “軽量 DI（依存性注入）” のようなもの  

〇 ServiceLoader とは何か  
ServiceLoader = “サービスインタフェースの実装クラスを、実行時に自動で見つけてロードする仕組み”  

Java には SPI（Service Provider Interface） という仕組みがあり、  
ServiceLoader はその SPI を実現するための標準 API。  




#コード例


■サービスインタフェースを定義する  

```
public interface Test {
    void execute();
}
```


■実装クラスを作る  

```
public class TestImpl implements Test {
    public void execute() {
        System.out.println("Hello");
    }
}
```


■ServiceLoader でロードする

```
ServiceLoader<Test> loader = ServiceLoader.load(Test.class);
```



■for-each で実装を取り出す  

```
for (Test t : loader) {
    t.execute();
}
```


