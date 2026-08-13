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