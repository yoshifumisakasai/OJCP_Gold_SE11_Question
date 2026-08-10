設問32

次のプログラムに関する説明として、正しいものを選べ（１つ）

```
Stream<Integer> a = Stream.of(1,2,3,4,5);
IntStream b = a.mapToInt(n -> n );
DoubleStream c = b.mapToDouble(n -> n);
Stream<Integer> d = c.mapToInt(n -> n);

```


A. 1行目でコンパイルエラーとなる


B. 2行目でコンパイルエラーとなる


C. 3行目でコンパイルエラーとなる


D. 4行目でコンパイルエラーとなる



#IntStream → Stream<Integer> への自動変換（オートボクシング変換）は存在しない。
理由：プリミティブストリームは「別物」であり、汎用 Stream と互換ではないため。


■なぜ自動変換されないのか？
① プリミティブストリームは「別の型階層」
**Java の Stream API には 2 系統ある：**

● 汎用ストリーム（参照型）
Stream<T>

● プリミティブストリーム（専用型）
・IntStream  
・LongStream   
・DoubleStream   
**これらは 継承関係がない。**  
**つまり IntStream は Stream<Integer> のサブクラスではない。**  


Stream<T>
↑ まったく別階層
IntStream
だから 代入できない。

② オートボクシングは「値の変換」であり「ストリーム型の変換」ではない
Java のオートボクシング：

int → Integer  
double → Double  
という 単一値の変換だけ。  

しかし今回必要なのは：
`IntStream → Stream<Integer>`  
という ストリーム型の変換。これはオートボクシングの範囲外。  

