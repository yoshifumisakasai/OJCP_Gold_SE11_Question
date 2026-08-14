設問77

次のプロパティファイルがある。このとき、次のプログラムを実行すると、どのプロパティファイルの内容が表示されるか、正しいものを選べ（１つ）


・sample.properties  
・sample_en.properties  
・sample_US.properties  
・sample_en_US.perperties  


```
import java.util.Locale;
import java.util.ResourceBundle;

public class Sample {

 public static void main(String[] args){
 
  Locale current = new Locale.Builder().setLanguage("en").build();
  ResourceBundle resource = ResourceBundle.getBundle("sample", current);
  System.out.println(resource.getString("hello"));
 }
}
```


A. sample.properties  


B. sample_en.properties  


C. sample_US.properties  


D. sample_en_US.perperties  


#ResourceBundle の探索順序  

（考え方）　最も具体的 → 徐々に一般化 → ルート” の順。


■標準的なフォールバック

1. 言語＋国＋バリアント

2. 言語＋国

3. 言語

4. ルート

