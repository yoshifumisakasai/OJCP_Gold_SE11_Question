設問49

次のプログラムを確認してください


```
var exe = Executors.newFixedThreadPool(5);
Future f = exe.submit(() -> 10);

```


submitメソッドの引数に渡すラムダ式は、どの関数型インタフェースで扱うことができるか。正しいものを選べ（１つ）


A. java.util.concurrent.Callable


B. java.lang.Ruunable


C. java.util.function.Function


D. java.util.function.Predicate


#Callableインタフェース

このラムダ式 () -> 10 は 戻り値があるので、扱える関数型インタフェースは Callable だけです。  


#submit のオーバーロード  
ExecutorService#submit には以下の2つ（オーバーロード）がある：


● ① Runnable を受け取る submit
`Future<?> submit(Runnable task)`  
Runnable は 戻り値なし（void run()）   
→ () -> 10 は戻り値があるので Runnable には一致しない  




● ② Callable を受け取る submit
`<T> Future<T> submit(Callable<T> task)`  
Callable ：
`V call() throws Exception;`  
→ 戻り値あり

() -> 10 は戻り値があるので Callable に一致する


---------------------------------------------------

■選択肢判定

B. Runnable
→ 戻り値なしの run() を要求
→ () -> 10 は戻り値があるので 不一致



C. Function
`R apply(T t)`  
→ 引数が必要
→ () ではなく (x) -> ... の形
→ 不一致



D. Predicate
`boolean test(T t)`  
→ 引数が必要
→ 戻り値は boolean
→ 不一致



#🎯 Future とは何か
別スレッドで実行した処理の「結果」「進行状況」「完了」を後から受け取るためのオブジェクト。  



◆ 1. Future が使われる場面

```
var exe = Executors.newFixedThreadPool(5);
Future f = exe.submit(() -> 10);
```

※submit() は 非同期でタスクを実行し、その結果を受け取るための Future を返す。  



◆ 2. Future の役割（3つの機能）
① 結果を受け取る

`Integer result = f.get();`  // 10 が返る
get() は「タスクが終わるまで待つ（ブロックする）」。



② タスクが終わったか確認する
`f.isDone();`     // 終わっていれば true


③ タスクをキャンセルする
`f.cancel(true);`
◆ 3. Future の内部イメージ（芳文向けに分解）
Future は「非同期処理の結果を保持する箱」。


Future<T>
 ├─ 実行中か？
 ├─ 終わったか？
 ├─ キャンセルされたか？
 └─ 結果（T）
submit() はタスクをスレッドプールに渡し、
そのタスクの状態を監視するための Future を返す。


◆ 4. Future の戻り値は Callable に依存する

`Future f = exe.submit(() -> 10);`  
() -> 10 は 戻り値ありなので Callable として扱われる。

Callable の call() の戻り値が Future.get() の結果になる。