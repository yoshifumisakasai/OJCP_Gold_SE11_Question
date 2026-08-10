設問9


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）



□コード1

```
public class TroubleResource implements AutoCloseable{

 @Override
 public void close() throws Exception{
 
  throw new RuntimeException("trouble");
 }
}
```

□コード2

```
public class TroubleMaker {

 public static void main(String[] args) {
 
  try ( TroubleResource a = new TroubleResource()){
  
   throw new Exception();
  
  } catch (RuntimeException e) {
  
   System.out.println("A");
  
  } catch (Exception e) {
  
   System.out.println("B");
  }
 }

}

```


A. 「A」と表示される


B. 「B」と表示される


C. コンパイルエラーが発生する


D. 実行時にエラーが発生し、プログラムが強制終了する



#説明

**close() が投げた RuntimeException が catch(RuntimeException) に捕まる**  


#処理順

1. try ブロック内で発生する例外  

`throw new Exception();`  
これは チェック例外（Exception）  


2. try-with-resources により close() が呼ばれる  
リソース a の close() が呼ばれる：  

`throw new RuntimeException("trouble");`  
close() が RuntimeException を投げる。  



#どちらの例外が「主例外」になるかの判定基準について
try-with-resources の仕様： 

・**try 内の例外（Exception） が「主例外」**  
・**close() の例外（RuntimeException）は suppressed（抑制例外） になる**  

つまり結論：  
`主例外：Exception`  
`抑制例外：RuntimeException("trouble")`  


#重要ポイント：close() の例外は「主例外を上書きする」場合がある点  
Java の仕様では、
try 内で例外が発生 → close() で別の例外が発生した場合、close() の例外が throw される  

つまり：
*try 内の Exception は 抑制される側*  
*close() の RuntimeException が 最終的に throw される*  

⇒catch(RuntimeException) が実行される。
