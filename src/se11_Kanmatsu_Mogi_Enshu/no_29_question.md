設問29

次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）

□コード1

```
public class SampleException extends Exception{

 public SampleException(String message){
 
  super(message);
 }
}

```

□コード2

```
public class TestException extends SampleException{

 public TestException(String message){
  super(message);
 }
}

```

□コード3

```
public class Sample {

 private static void test() throws TestException{
 
  try{
     // do something
     throw new TestException("A");
     
  }catch(SampleException | RuntimeException e){
   throw new RuntimeException("B");
  }
 } 

public static void main(String[] args){

 try{
   test();
 
 } catch(Exception e){
    System.out.println(e.getMessage());
 
  }
 }
}

```


A. 「A」と表示される

B. 「B」と表示される

C. 何も表示されない

D. コンパイルエラーが発生する



#処理の流れ
**例外の継承関係 → マルチキャッチ → 再スロー → main で捕捉 → メッセージ表示という流れ**  


◆ 1. test() 内の try ブロックで例外が発生する
`throw new TestException("A");`  
ここで TestException("A") が投げられる。




◆ 2. catch に入るか？
catch はこうなっている：

`catch (SampleException | RuntimeException e)`  
そして継承関係は：

`TestException extends SampleException`  
つまり TestException は SampleException のサブクラス  
→ catch(SampleException | …) に捕まる。



◆ 3. catch ブロックの中身
`throw new RuntimeException("B");`  
ここで RuntimeException("B") が再スローされる。




◆ 4. main の catch に届く

```
catch (Exception e) {
    System.out.println(e.getMessage());
}
```

RuntimeException は Exception のサブクラスなので捕まる。




◆ 5. 表示されるメッセージ
java
e.getMessage()  // "B"
よってコンソールには：

コード
B
と表示される。
