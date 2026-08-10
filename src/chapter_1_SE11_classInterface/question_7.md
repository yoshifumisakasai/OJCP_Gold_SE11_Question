設問7


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


□コード1

```

public class Sample{

 private int num;
 public Sample(int num){
  this.num = num;
 
 }
 
 public int getNum(){
 
  return num;
 }
 
 public void setNum(int num){
  this.num = num;
 }

}
```


□コード2


```
public class Main{

 public static void main(String[] args){
 
  var sample = new Sample(10){
  
   void modify(int num){
    setNum(num);
   }
  
  };
  
  sample.modify(100);
  System.out.println(sample.getNum());
 }

}

```

A. 「10」と表示される

B. 「100」と表示される

C. コンパイルエラーが発生する

D. 実行時に例外がスローされる

