設問6

try-with-resourcesの記述として、正しいものを選べ（１つ）


A. try ( A a = new A()){
    //do something

   }
   
   
   
B. B b = null;
     try ( b = new B()){
       // do something
    }
    
    
C. C c = new C());
   try (c) {
    // do something
   
   }
   
   
D. try ( D d = new D()){
     d = new D();

   }
   
   
E. E e = new E());

   try (e) {
   
    // do something
   
   }
   e = new E();
 
 
 
#試験で問われる try-with-resources の構文ルール  

・**括弧内は AutoCloseable を実装した変数の宣言＋初期化のみ** 
(変数名だけを書くことはできない)   

・**事前に宣言した変数は使えない**  

・**変数は 実質 final（再代入不可）**  


`AutoCloseable（または Closeable）を実装していれば OK`  
↓↓  

try-with-resources に置けるリソースは AutoCloseable を実装したクラスであり、Closeable は AutoCloseable を継承しているため、当該クラス（設問では、クラスAやクラスB、クラスC、クラスD、クラスEなど）が AutoCloseable または Closeable のどちらかを implements していれば OK　　

 