設問8

次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


□コード1

```
public interface Test {

 public default void execute(String str){
 
  System.out.println("A");
 }
}

```

□コード2


```

public abstract class AbstractTest{

 private void execute(String str){
 
  System.out.println("B");
 }

}
```


□コード3


```

public class Sample extends AbstractTest implements Test {

 public static void main(String[] args){
 
  new Sample().execute("hello");
 }
}
```


A. 「A」と表示される


B. 「B」と表示される


C. コンパイルエラーが発生する


D. 実行時に例外がスローされる


#ポイント
**抽象クラス（abstract class）は “抽象メソッドだけ” ではなく、普通のメソッド（実装あり）も書ける。**  



#メソッド探索の優先順位  

🔍 メソッド探索の優先順位（Java の仕様）
Java のメソッド探索は以下の順番で行われる：  

(1) そのクラス自身にあるメソッド  

(2) 親クラス（super class）にあるメソッド  

(3) インタフェースの default メソッド  

ただし：
private メソッドは継承されない  
つまり「親クラスの private メソッド」は探索対象に入らない  
