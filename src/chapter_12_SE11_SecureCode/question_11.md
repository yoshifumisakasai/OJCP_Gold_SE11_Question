設問11

SQLインジェクションを防ぐために使用するインタフェースとして、正しいものを選べ（１つ）

A. java.sql.Statement


B. java.sql.PreparedStatement


C. java.sql.CallableStatement


D. java.sql.SecureStatement



#PreparedStatement
SQLインジェクション対策として最も重要なのは「SQL文とパラメータを分離する」こと。



□(PreparedStatement はまさにそのための仕組)  


```
① SQL を事前コンパイル  

② ? プレースホルダに値を安全にバインド  

③ 文字列連結による危険な SQL 組み立てを防止  
```

という特徴を持つため、SQLインジェクション対策の標準手段  



A. Statement
**SQL を文字列連結で組み立てるため、インジェクションの危険が高い**  

C. CallableStatement 
→ **ストアドプロシージャ呼び出し用**  
*PreparedStatement と同様にパラメータバインドはできるが、SQLインジェクション対策の主目的で使うインタフェースではない*  

