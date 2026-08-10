設問20


次のコードのうち、正しく記述されているものを選べ（１つ）


A. Ruunable a = {System.out.println("helllo. ")};


B. Runnable b = "hello" -> System.out.println();


C. Runnable c = () -> {System.out.println("hello");};


D. Runnable d = () -> System.out::print;


E. Runnable e = -> System.out.println("hello. ");



#Runnableインタフェース
**引数なし・戻り値なし（void run()）の関数型インタフェース**  
**ラムダ式は () -> ... の形でなければならない**  


Runnable の抽象メソッド：
`void run();`

・引数なし → ()  

・戻り値なし → { ... } または式  
