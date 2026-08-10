設問10

次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）

□コード1

```

public interface Sample{

 static void test(){
 
  System.out.println("A");
 }
}

```


□コード2

```

public class SampleImpl implements Sample {


 public static void test(){
 
  System.out.println("B");
 }
 
 public static void main(String[] args){
 
  Sample.test();
 }
}

```


A. 「A」と表示される


B. 「B」と表示される


C. コンパイルエラーが発生する


D. 実行時に例外がスローされる




#まず最重要ポイント
**インタフェースの static メソッドは「継承されない」し「オーバーライドできない」**  
**呼び出せるのは “宣言したインタフェース名” のみ**  



※SampleImpl にも static メソッド test() があるが、これは インタフェースの static メソッドとは別物  



■Java の仕様：  

```
static メソッドは オーバーライド不可  

static メソッドは 継承されない  

呼び出しは 宣言元の型名でのみ可能  
```

※Sample.test() は 常にインタフェース Sample のメソッド  

