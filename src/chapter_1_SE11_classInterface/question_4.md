設問4


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


```
public class Outer {

 private int num = 2;
 public void hoge() {
 
  Inner test = new Inner();
  test.data =100;
  test.execute();
 
 }
 
 
 private static class Inner {
 
  private int data;
  void execute(){
   System.out.println(num + data);
  
  }
 
 }

}

```


A. 5行目でコンパイルエラーが発生する


B. 11行目でコンパイルエラーが発生する


C 「200」と表示される


D. 実行時に例外がスローされる


#ポイント
**「static ネストクラスは外側インスタンスの非 static フィールドにアクセスできない」**  
**“非 static インナークラスは Outer の this が必要” の逆パターン**  


〇 *Inner は static ネストクラス*

`Outer のインスタンスに紐づかない`  

`Outer の this を持たない`  

`Outer の非 static フィールドにアクセスできない`  

⇒**num にアクセスするための Outer の this が存在しない**  


