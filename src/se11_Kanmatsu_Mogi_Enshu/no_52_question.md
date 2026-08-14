設問52

次のプログラムはコンパイルエラーとなる。コンパイルエラーを解消するための方法として、正しいものを選べ（2つ）


```

public class Sample {

 public static void main(String[] args){
 
  var subject = new Subject("A");
  
 }
 
 class Subject {
 
  String name;
  Subject(String name){
  
   this.name = name;
  }
 }

}

```


A. Subjectクラスの宣言をstaticで修飾する


B. Subjectクラスの宣言自体を、インナークラスではなく別のクラスと指定定義する


C. mainメソッド内の「var subject」を「Subject subject」に変更する


D. Subjectクラスのコンストラクタをpublicにする


E. Subjectクラスをpublicで宣言する




#非 static インナークラスを main から new できない理由

■切り分けポイント
・main が static であること  
＆
・Subject が非 static インナークラスであること。  


-----------


〇コンパイルエラーの原因（まずここを押さえる）
`class Subject { ... }`  

-------  
・Sample の非 static インナークラス。  
・main は static：  
-------  

`public static void main(String[] args)`  
**static メソッドから 非 static インナークラスを new するには、外側インスタンスが必要。** 

つまり：
main から Subject を new するには、new Sample().new Subject("A")の形が必要。

しかしコードは：
var subject = new Subject("A");
→ 外側インスタンスがないため コンパイルエラー。  




#選択肢判定

A. Subjectクラスの宣言をstaticで修飾する
static class Subject { ... }  
✔ static にすれば 外側インスタンス不要      
✔ main から new Subject("A") が可能になる  


B. Subjectクラスの宣言自体を、インナークラスではなく別のクラスとして定義する  
✔ Subject を Sample の外に出せば、普通のトップレベルクラスになる  
✔ main から new Subject("A") が可能  