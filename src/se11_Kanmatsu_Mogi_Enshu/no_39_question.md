設問39

次のクラスをスレッドセーフにするためには、何をするべきか、正しいものを選べ（１つ）


```
import java.util.concurrent.locks.ReentrantLock;


public class Sample {

 private final ReentrantLock lock = new ReentrantLock();
 
 public void test() throws Exception {
 
  try {
     lock.lock();
     // do something
  } finally {
     lock.unlock();
  }
 
 }

}
```


A. lockフィールドの宣言をtestメソッド内に移動する


B. ReentrantLockのコンストラクタにtrueを渡す


C. lockフィールドの宣言をstaticにする


D. 変更は必要ない


#スレッドセーフになる理由

■本コードで実現される機能（↓↓）  

・インスタンスごとに 1 つの lock を持つ（final）

・lock.lock() で排他制御

・finally で必ず unlock()（例外が出ても確実に解放）

・ReentrantLock は 同じスレッドが再取得可能（再入可能）



⇒正しい排他制御  



----------------------------------

B. ReentrantLockのコンストラクタにtrueを渡す
→ new ReentrantLock(true) は 公平ロック（Fair lock）  → スレッドセーフ性とは無関係


C. lockフィールドの宣言をstaticにする
→ 全インスタンスで lock を共有することになる、必要な場面もあるが、このコードでは不要　　
→ スレッドセーフ性のために static は必須ではない　　


A. lockフィールドの宣言をtestメソッド内に移動する
→ 毎回新しい lock を作ることになる→ 排他制御にならない（意味がなくなる）　　
