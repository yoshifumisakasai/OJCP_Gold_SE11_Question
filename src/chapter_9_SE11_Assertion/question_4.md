設問4

try-with-resourcesの説明として、正しいものを選べ（１つ）

A. catchブロックは必須である


B. finallyブロックは必須である


C. catchブロックかfinallyブロックのどちらかを記述しなければならない


D. try-with-resourcesの主な目的は例外処理ではない


E. 選択肢A～Dはすべて誤りである



#ポイント
**try-with-resources の主目的は「例外処理」ではなく「リソースの確実な解放（close の自動化）」**   


*・catchブロックは必須ではない*  
*・finallyブロックは必須ではない*  
**try-with-resources は try 本体だけで成立する**

```
try (var br = new BufferedReader(...)) {
    ...
}
```

finally を書かなくても 自動で close() が呼ばれる  

