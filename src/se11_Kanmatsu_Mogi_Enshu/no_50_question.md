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
