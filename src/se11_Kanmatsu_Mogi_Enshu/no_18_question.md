設問18

次のようなコンソールで動作するアプリケーションを開発している。


```
public class Sample {

 public static void main(String[] args){
 
  Console console = System.console();
  var name = console.readLine("name > ");
  var pass = console.readPassword("pass > ");
  System.out.println("name : " +name+",pass: " + String.valueOf(pass));
 }

}

```


ユーザとのやり取り、および結果の表示として、正しいものを選べ。なお、nameにはsample、passにはpassowrdと入力しているものとする（１つ選べ）


A. name > sample
   pass > password
   name : sample, pass:password
   
   
B. name > sample
   pass > password
   name : sample, pass: [C@4f6abcdef
   
C. name > sample
   pass > 
   name : sample, pass:password
   
D. name > sample
   pass > 
   name : sample, pass:



# 仕様ポイント 
Console.readPassword() は入力した文字を画面に表示しない（非エコー） かつ
戻り値は char[] であり、String.valueOf(char[]) は配列の内容ではなく配列の toString() を返す  
という 2 つの仕様がポイント


   ③ String.valueOf(pass)
pass は char[] なので、String.valueOf(char[]) ：
配列の内容ではなく
配列の toString()（例： [C@4f6abcdef）を返す

String.valueOf(pass) → "password"（配列の中身を文字列化）
"pass: " + pass → pass: [C@4f6abcdef]（配列の toString()）


-------------------------------

#説明  

実際にどう動くかをコードで確認
■1. String.valueOf(char[]) の仕様  
Java の公式仕様：  


`String.valueOf(char[] data)`  
⇒char 配列の内容をそのまま文字列にする。

例：

```
char[] arr = {'p','a','s','s'};
System.out.println(String.valueOf(arr));
```
出力：
pass
つまり 配列の中身がそのまま文字列になる。

■配列をそのまま文字列連結するとどうなるか？
`char[] arr = {'p','a','s','s'};`  
`System.out.println("pass: " + arr);`
出力：
コード
pass: [C@4f6abcdef

理由：
・配列はオブジェクト  
・文字列連結すると arr.toString() が呼ばれる  

**配列の toString() は「型 + @ + ハッシュコード」形式**  
例：[C@4f6abcdef