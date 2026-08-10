設問15

次のプログラムをコンパイル、実行したときコンソールに「A」と表示したい。
insert code hereに記述するコードとして、正しいものを選べ（１つ）


□コード1

```
public enum Test{

A, B, C
}

```



□コード2


```

public static void main(string[] args){


 // insert code here
}

```


A. System.out.println(Test.values()[0]);

B. System.out.println(Test.values(0);

C. System.out.println(Test.values()[1]);

D. System.out.println(Test.values(1));

E. System.out.println(Test.valueOf(1));

F. System.out.println(Test.valueOf()[1]);

A. System.out.println(Test.values()[0]);



#ポイント

**enum Test { A, B, C } の定義では、定数は 0 から順にインデックスが振られる**  

`Test.values() `  
⇒enum の定数を配列として返す  

`Test.values()[0]`  
 // A  
⇒これを println すると "A" が表示  

