設問50

次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


```
IntStream stream = IntStream.iterate(0, a -> a + 1);
stream.limit(5)
.mapToObj(x -> x + ",")
.forEach(System.out::print);

```


A. 「1,2,3,4,5」と表示される


B. 「0,1,2,3,4」と表示される


C. 「0,1,2,3,4,」と表示される


D. 「1,2,3,4,5,」と表示される


E. コンパイルエラーが発生する



#コード解説

① `IntStream.iterate(0, a -> a + 1)`  
無限ストリームを生成  

要素は 0, 1, 2, 3, 4, 5, ...  



② `.limit(5)`  
最初の 5 要素だけに制限  

要素は 0, 1, 2, 3, 4  



③ .mapToObj(x -> x + ",")  
各要素を文字列に変換  

結果は "0," "1," "2," "3," "4,"  


■「mapToObj」補足
`<R> Stream<R> mapToObj(IntFunction<? extends R> mapper)`  
ジェネリック型パラメータ <R> がある  

引数は IntFunction<? extends R>  

戻り値は Stream<R>  

※**戻り値型 R は、ラムダ式（mapper）の戻り値型からコンパイラが推論する。**  
