
設問14


次のプログラムの、「insert code here」に記述して、コンパイルができるコードとして、正しいものを選べ（１つ）


コード

```
public interface Sample {
 //insert code here
}


```


A. private void a();


B. private void b() {

 // do something
}


C. private default void c(){

 // do something
}


D. 上記の選択肢はいずれもコンパイルエラーとなる




#Javaルール

インタフェース内で private メソッドを宣言できるのは Java 9 以降だが、
その場合は **必ず本体（ブロック）を持つ必要がある**  
*抽象メソッド（セミコロンのみ）は private にできない*  


```
private は OK  

default と private の組み合わせは 禁止

抽象メソッドに private は 禁止（抽象メソッドは外部から呼ばれる前提なので private にできない）
```

これらのルールにより、選択肢 A〜C はすべてコンパイルエラー  


