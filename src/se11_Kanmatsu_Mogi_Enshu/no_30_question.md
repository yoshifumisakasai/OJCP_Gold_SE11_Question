設問30

sample.txtが存在しない場合、次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


```
import java.io.IOException
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;


public class Sample {

public static void main(String[] args){

 try{
  Path path = Paths.get("sample.txt");
  boolean result = Files.deleteIfExists(path);
  if(result){
   System.out.println("A");
  
  }else {
   System.out.println("B");
  }
 
 }catch (IOException e){
  System.out.println("C");
 }
}


}

```


A. 「A」と表示される


B. 「B」と表示される


C. 「C」と表示される


D. コンパイルエラーが発生する


E. 実行時に例外がスローされる




#1. Path の生成

`Path path = Paths.get("sample.txt");`  
**これは単にパスを表すだけで、存在チェックはしない。**  



#◆ 2. deleteIfExists の動作  
`boolean result = Files.deleteIfExists(path);`  

JavaDoc：  
**ファイルが存在する → 削除して true**  
**ファイルが存在しない → false**  
**削除中に I/O エラー → IOException** 

今回の前提：  
sample.txt が存在しないので戻り値は false。  
