設問61

次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）
なお、srcとdestは存在するものとする。


```
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class Sample {

 public static void main(String[] args){
 
  Path src = Paths.get("a/sample.txt");
  Path dest = Paths.get("dest");
  Files.move(src, dest);
 }
}

```

A. a/sample.txtのコピーがdestディレクトリに作られ、a/sample.txtが削除される


B. sample.txtの名前がdestに変更される


C. java.nio.file.FileAlreadyExistsExceptionがスローされる


D. java.nio.file.NoSuchFileExceptionがスローされる


E. コンパイルエラーとなる



#ポイント

Files.move(src, dest) は コピーではなく「移動」＋「リネーム」 を行います。  
dest は ディレクトリではなくファイル名 として扱われる  

`a/sample.txt → dest`  
ファイル名変更（リネーム）   


・src は既存のファイル：a/sample.txt  
・dest は「ディレクトリ」ではなく「ファイル名」として扱われる  
→ dest が既存ディレクトリかどうかは関係ない 
→ ディレクトリとして扱うには、dest/sample.txt のようにパスを指定する必要がある 

■実際の動作：  

・a/sample.txt が dest という名前に変更される
・元の a/sample.txt は削除される（移動） 

