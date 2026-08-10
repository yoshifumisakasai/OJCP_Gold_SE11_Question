設問5

try-with-resources文で自動的に閉じられるリソースを定義することができるのは、次のうちどれか。正しいものを選べ（１つ）


A. java.io.Closeableインタフェースを実装したクラスのみ


B. java.lang.AutoCloseableインタフェースを実装したクラスのみ


C. java.io.Closeableインタフェースとjava.lang.AutoCloseableインタフェースを実装したクラスのみ


D. java.io.Closeableインタフェースとjava.lang.AutoCloseableインタフェースのいずれかを実装したクラスのみ



#学習ポイント

**try-with-resources に入れられるリソースは AutoCloseable を実装したクラス**  
**Closeable は AutoCloseable を継承しているため、Closeable でも OK、AutoCloseable でも OK**  



■インタフェースAutoCloseable  
`public interface AutoCloseable`  



■インタフェースCloseable  
`public interface Closeable extends AutoCloseable`  

