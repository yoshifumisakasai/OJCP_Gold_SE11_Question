設問40

次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）。
なお、変数dsはjavax.sql.DataSource型のオブジェクトであり、TEST表が正しく定義されているものとする。


```

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.DataSource;

public class Sample {

 public static void main(String[] args) throws Exception {
 
  // do something
  
  
  try (Connection con = ds.getConnection();
  PreparedStatement ps = con.preparedStatement("INSERT INTO TEST VALUES (?,?)")){
  
  ps.setInt(1, 100);
  ps.setString(2, "SAMPLE");
  ps.executeUpdate();
  ps.setInt(1, 101);
  ps.executeUpdate();
  }
 
 }
}

```

A. 「100, "SAMPLE"」および「101, NULL」という2つの行が挿入される


B. 「100, "SAMPLE"」という1つの行が挿入される


C. 「100, "SAMPLE"」および「101, "SAMPLE"」という2つの行が挿入される

D. 実行時に例外がスローされる

E. コンパイルエラーが発生する




#なぜ「101, NULL」になるのか（ポイント)

**PreparedStatement は 前回セットしたパラメータを保持しない。**  


□フロー：  

ps.setInt(1, 100) → 1番目の「?」に 100 をセット
ps.setString(2, "SAMPLE") → 2番目の「?」に SAMPLE をセット
ps.executeUpdate() → 1行目挿入（100, SAMPLE）


□フロー次：

ps.setInt(1, 101) → 1番目の「?」だけを 101 に変更
**2番目の「?」は再セットしていない**  

`PreparedStatement は パラメータを自動的に保持し続けるわけではないため、2番目の「?」は 未設定（＝NULL） になる。`  