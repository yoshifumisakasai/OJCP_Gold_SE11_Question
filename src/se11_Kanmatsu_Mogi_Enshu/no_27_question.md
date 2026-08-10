設問27

次のプログラムの「here」の行を実行したときの状態に関する説明として、正しいものを選べ（１つ）


```
import java.io.FileReader;
import java.io.IOException;
import java.io.Reader;


public class Sample {

 public static void main(String[] args){
 
  try (
  
    Reader a = new FileReader("sample1.txt");
    Reader b = new FileReader("sample2.txt");
    Reader c = new FileReader("sample3.txt")){
    
  }catch (IOException e) {
    // do something
  }
  
  // here
 }

}


```

A. コンパイルエラーが発生する


B. aのみが閉じられる


C. 3つのReaderオブジェクトがすべて閉じられる


D. 3つのReaderオブジェクトはすべて開いたままである


E. 実行時に例外がスローされる



# try-with-resources の基本ルール

◆ try-with-resources の基本ルール  
`try (resource1; resource2; resource3) { ... }`  

**この形式で宣言されたリソースは、try ブロックを抜けるときに自動的に close() が呼ばれる。呼ばれる順番は 逆順（LIFO）**  

今回のコード：

```
try (
    Reader a = new FileReader("sample1.txt");
    Reader b = new FileReader("sample2.txt");
    Reader c = new FileReader("sample3.txt")
) {
} catch (IOException e) {
}
```

*ここで宣言された a, b, c はすべて AutoCloseable なので、try ブロック終了時に 必ず close() が呼ばれる。*  



#AutoCloseable とは何か？  
◆ AutoCloseable は「自動 close できるリソース」を表すインタフェース  

```
public interface AutoCloseable {
    void close() throws Exception;
}
```
つまり：

・close() を持つ  
・try-with-resources に入れると自動で close() が呼ばれる  
・Java 7 で導入された  


#なぜ Reader が AutoCloseable と分かるのか？  
Java の Reader クラス階層：

```
AutoCloseable
   ↑
Closeable
   ↑
Reader
   ↑
FileReader
```

ポイントは Closeable が AutoCloseable を継承していること。

```
public interface Closeable extends AutoCloseable {
    void close() throws IOException;
}
```
つまり：
・FileReader は Reader のサブクラス  
・Reader は Closeable を実装  
・Closeable は AutoCloseable を継承  

→ FileReader は AutoCloseable になる