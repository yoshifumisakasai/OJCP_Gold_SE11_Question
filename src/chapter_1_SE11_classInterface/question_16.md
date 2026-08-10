設問16

次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


□コード1

```
public enum Sample {

 A("hello"), B("hello"), C("hello");
 
 private final String value;

 private Sample(String value){
 
  System.out.println(value);
  this.value = value;
 }
 
 @Override
 public String toString(){
  return this.value;
 }

}

```


□コード2

```
public static void main(String[] args){

 System.out.println(Sample.A);
}

```


A. 「A」と表示される

B. 「hello」が1回表示される

C. 「hello」が3回表示される

D.  「hello」が4回表示される



#enum の各定数（A, B, C）は クラスのインスタンスとして生成される。
そのため コンストラクタは定数の数だけ呼ばれる。  

`A("hello"), B("hello"), C("hello");`  
**3 つの定数が クラス Sample のインスタンスとして生成される**  


〇コンストラクタ  

```
private Sample(String value){
    System.out.println(value);
    this.value = value;
}
```

**定数が生成されるタイミングで コンストラクタが 3 回呼ばれる**  
