設問15

try-with-resources文で扱うクラスに関する説明として、正しく記述されているものを選べ（１つ）


A. AutoCloseableを実装し、autoCloseメソッドをオーバーライドする



B. AutoCloseableを継承し、closeメソッドをオーバーライドする



C. AutoCloseableを継承し、autoCloseメソッドをオーバーライドする


D. AutoCloseableを実装し、closeメソッドをオーバーライドする



#ポイント
**try-with-resources が扱えるのは AutoCloseable を実装していて、close() を持つクラス** 


■try-with-resources が要求する条件  
Java の仕様（JLS）では：

・try-with-resources に置けるリソースは AutoCloseable を実装したクラス  
・そして close() メソッドを持つこと  

〇AutoCloseable の定義：  

```
public interface AutoCloseable {
    void close() throws Exception;
}
```
つまり：  

autoClose というメソッドは存在しない  
close() をオーバーライドする必要がある  