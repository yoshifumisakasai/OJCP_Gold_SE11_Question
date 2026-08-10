設問14

以下に示すプログラムの「insert code here」に記述するコードとして、適切なものをAとBのどちらか。またその理由と共に正しい記述を選択肢より選べ（１つ）



A: "SELECT * FROM TABLE WHERE NAME = " + name
B: "SELECT * FROM TABLE WHERE NAME = " + stmt.enquoteIdentifier(name, true);


□コード

```
import java.sql.Connection;
import java.sql.SQLException;
import java.sql.Statement;


public class Sample {

 public void execute(Connection con, String name) throws SQLException{
 
  Statement stmt = con.createStatement();
  String sql = /*insert code here*/;
  stml.execute(sql);
 }
}

```

A. B:呼び出し側のコードが提供する値はすべて引用符で閉じる必要がある
B. A:呼び出し側のコードが提供するnameの値が正確に送られる
C. B:呼び出し側のコードが提供する値を引用符で閉じるとSQLインジェクションが防止される
D. AとBは機能的に等価である
E. 識別子を引用符で閉じる必要はない



#SQLインジェクション
「外部から渡された文字列をそのまま SQL に埋め込むことで、攻撃者が意図しない SQL を実行できてしまう脆弱性」。  



■具体例（これが一番理解しやすい）
`String sql = "SELECT * FROM users WHERE name = '" + name + "'";`  
攻撃者が name に次を入力すると：  
コード
`' OR '1'='1`  
実際に実行される SQL：
`SELECT * FROM users WHERE name = '' OR '1'='1'`  
→ WHERE 条件が常に true になる    
→ 全ユーザ情報が漏洩する  
これが SQLインジェクション。  
 

#Java でのSQLインジェクション防止方法
1. PreparedStatement を使う  

```
PreparedStatement ps = con.prepareStatement(
    "SELECT * FROM users WHERE name = ?"
);
```
ps.setString(1, name);  
SQL と値を分離  

値は「データ」として扱われ、SQL として解釈されない  
SQLインジェクション完全防止  
  

✔ 2. JDBC の enquoteIdentifier / enquoteLiteral を使う

`stmt.enquoteLiteral(name);`  
値を安全に引用符で囲む  
特殊文字をエスケープ  
SQLインジェクションを防止  
