設問37


次のプログラムを実行し、コンソールに「2」と表示したい。
「insert code here」に記述するコードとして、正しいものを選べ（１つ）


□コード1

```
public enum Type {

 A(1), B(2), C(3);
 int num;
 
 Type(int num) {
 
  this.num = num;
 }
 
 // insert code here

}

```


□コード2

```

public class Sample {

 public static void main(String[] args){
 
  System.out.println(Type.values()[1]);
 }
}

```


A. public String toString(){

    return String.valueOf(Type.values()[1]);
}


B. public String toString(){

    return "2";
}


C. public String toString(){

    return String.valueOf(A.num);
}

D. public String toString(){

    return String.valueOf(num);
}



#enum の toString をオーバーライド  

**ポイントは「System.out.println(Type.values()[1]) が何を呼ぶか」。**  

□実行されるコードの流れ

`System.out.println(Type.values()[1]);`  
Type.values()[1] は B を指す。

(補足）
Type.values()[1] が B を指す理由は「enum の定義順に 0 からインデックスが付く」　

↓↓↓↓↓↓

■ enum の定義順 = values() の順番  

```
public enum Type {
    A(1), B(2), C(3);
}
```
**Java の enum は 宣言した順番で内部的に配列に格納される。**  


enum の toString() をオーバーライドすると、
System.out.println(B) は B の toString() の戻り値を表示する。


つまり、B インスタンスのフィールド num（2）を返せばよい（↓↓）

※insert code hereに書くべきコード：  

```
public String toString(){
    return String.valueOf(num);
}
```