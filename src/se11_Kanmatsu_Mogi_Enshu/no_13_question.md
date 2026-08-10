設問13

次のプログラムを実行したときに、コンソールに出力される結果として、正しいものを選べ（１つ）


```
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.format.FormatStyle;
import java.util.Locale;


public class Sample {

 public static void main(String[] args){
 
  Locale l = new Locale("en", "US");
  LocalDate today = LocalDate.of(2021, 4, 1);
  String mToday = today.format(DateTimeFormatter.ofLocalizedDate(FormatStyle.MEDIUM).withLocale(l));
  String aToday = today.format(DateTimeFormatter.ofLocalizedDate(FormatStyle.SHORT).withLocale(l));
  System.out.println(mToday);
  System.out.println(aToday);
  
 }


}
```


A. 4/1/21
   Apr 1, 2021
   

B. Apr 1, 2021
   4/1/21

C. Thursday, April 1, 2021
   Apori 1, 2021
   
  
D. April 1, 2021
   4/1/21
   
   
   
#ポイント

■FormatStyle.MEDIUM（中くらいの長さ）  
英語（米国）：  

出力）  
Apr 1, 2021  
月は短縮（Apr）  
日は数字  
年は4桁  




■FormatStyle.SHORT（短い形式）   
英語（米国）：  

出力）  
4/1/21  
月/日/年（2桁）  

区切りはスラッシュ  

