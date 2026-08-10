設問7

特定のjarファイルだけに、セキュリティ上の特権を与えたい。セキュリティポリシーファイルの記述として、正しいものを選べ（１つ）

A. grant {
    permission java.security.AllPermission;
   };
   
   
B. grant base "file:/Users/shiga/workspace/chap12/lib.jar" {
    permission java.io.FilePermission "/", "read"; 
   };
   
   
C. grant jar "file:/Users/shiga/workspace/chap12/lib.jar" {
    permission java.io.FilePermission "/", "read"; 
   };
   
   
D. grant codeBase "file:/Users/shiga/workspace/chap12/lib.jar" {
    permission java.io.FilePermission "/", "read"; 
   };
   
   
#codeBase
Java のセキュリティポリシーファイルで特定の JAR にだけ権限を与える場合、記述は次の形式になる：  

```
grant codeBase "file:/path/to/xxx.jar" {
    permission ...;
};
```

**codeBase が 「この JAR（コードベース）に対して権限を与える」という意味**  
