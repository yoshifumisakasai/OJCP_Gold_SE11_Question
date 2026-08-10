設問8

try-with-resourcesのtryブロック内で例外が発生したとき、リソースのクローズ、catchブロック、finallyブロックはどの順番で実行されるか。正しい順番となっているものを選べ（１つ）


A. finally、catch、close


B. close、catch、finally


C. catch、finally、close


D. catch、close、finally


#try-with-resources の 例外発生時の実行順序

1.close（リソースのクローズ）  
↓  
2.catch（例外処理）  
↓  
3.finally（最後の後処理）  


**実際は close が finally の中で先に実行される**  



#コンパイラが生成するコード(概念的)：

```
Throwable primary = null;
try {
    // try本体
} catch (Throwable t) {
    primary = t;
    throw t;
} finally {
    try {
        resource.close();  // ← ここが最初に呼ばれる
    } catch (Throwable suppressed) {
        primary.addSuppressed(suppressed);
    }
}
```

**つまり：例外が発生したらまず close() が呼ばれる**  

