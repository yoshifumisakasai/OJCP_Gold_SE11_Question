設問51

以下のパッケージが含まれるjarファイルを使用するJava8ベースのアプリケーションがある。

・com.sample.test
・com.sample.hello
・com.sample.boo

このjarファイルをモジュール化して、test、hello、booという3つのモジュールにするためには、どのようにモジュール定義ファイルを記述すればよいか。正しいものを選べ（１つ）



A. module com.sample.test {
    provides com.sample.test;

   }
   
   module com.sample.hello {
    provides com.sample.hello;

   }
   
   module com.sample.boo {
    provides com.sample.boo;

   }
   
   
B. module com.sample.test {
    opens com.sample.test;

   }
   
   module com.sample.hello {
    opens com.sample.hello;

   }
   
   module com.sample.boo {
    opens com.sample.boo;

   }
   
   
C. module com.sample.test {
    requires com.sample.test;

   }
   
   module com.sample.hello {
    requires com.sample.hello;

   }
   
   module com.sample.boo {
    requires com.sample.boo;

   }
   
   
D. module com.sample.test {
    exports com.sample.test;

   }
   
   module com.sample.hello {
    exports com.sample.hello;

   }
   
   module com.sample.boo {
    exports com.sample.boo;

   }