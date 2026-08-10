設問35

次のプログラムをDoS攻撃から保護するための方法として、正しいものを選べ（１つ）

```
import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;
import java.io.Reader;
import java.util.ArrayList;
import java.util.List;


public class Sample {

 public static void main(String[] args){
 
  List<Reader> list = new ArrayList<>();
  File file = new File("sample.txt");
  
  try (BufferedReader br = new BuffereedReader(new FileReader(file))){
  
   for(String fileName = br.readLine();
   fileName != null; fileName = br.readLine()){
   
    BufferedReader br2 = new BufferedReader(new FileReader(fileName));
    list.add(br2);
    process(br2);
   }
  
  }catch (IOException e) {
  
  } finally {
  
   for(Reader r : list){
   
   try {
    r.close();
   
   }catch (IOException ex){
   
    // do something
   }
  
  }
 }
}
private static void process(BufferedReader br2){

 // do something
}
}

```

A. br2を生成するタイミングで、try-with-resourcesを使う


B. processメソッドの実行後に、br2.closeメソッドを呼び出す


C. processメソッドの呼び出し時に、try-with-resourcesを使う


D. br2を生成する前に、brのサイズをチェックして、容量をオーバーしないかを確認する


E. finallyブロックに、「br.close();」を記述する


#このコードの「危険ポイント」を整理する

◆ br2（BufferedReader）が大量に生成される可能性  

```
BufferedReader br2 = new BufferedReader(new FileReader(fileName));
list.add(br2);
process(br2);
```

sample.txt に大量のファイル名が書かれていたら
→ br2 が 無限に生成される
しかも list に溜め続ける

finally でまとめて close しているが→ close が遅すぎる（DoS攻撃の典型的な弱点）

つまり、攻撃者が巨大なファイルを渡すと：

・Reader が大量に生成される  
・OS のファイルディスクリプタが枯渇する  
・JVM が止まる（DoS）    


#どこを改善すべきか？
br2 を生成したら すぐに close すべき  

```
try (BufferedReader br2 = new BufferedReader(new FileReader(fileName))) {
    process(br2);
}
```

これが 最も正しい DoS対策。
**br2を生成するタイミングで、try-with-resourcesを使う**  

⇒*br2 を即 close できるため、大量の Reader が溜まらず、リソース枯渇を防げる。*  
