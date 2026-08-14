設問75


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


```
import java.util.List;
import java.util.stream.IntStream;

public class Sample {

 public static void main(String[] args){
 
  final List<String> list = List.of("A", "B", "C", "D");
  final List<String> list2 = List.of("D", "E", "F", "G");
  
  IntStream
  .range(0, Math.min(list.size(), list2.size()))
  .mapToObj((i) -> list.get(i)+ " "+ list2.get(i))
  .forEach(System.out::println);
 }

}

```

A. 何も表示されない


B. 「A D」「B E」「C F」「D G」と表示される


C. 「A D」と表示される


D. コンパイルエラーとなる。



#ポイント

Math.min メソッドは、2つの値を比較して小さい方の値を返します。このメソッドは、int、long、float、double 型に対応しています。　　
※（Java の Math.min() メソッドは、2つの引数が同じ値の場合、その値をそのまま返します。
つまり、比較結果が「どちらも同じ」なら、単純にその値が返るだけです。）  

IntStream.range は、指定した開始値（含む）から終了値（含まない）までの連続した整数を生成するメソッドです。　　



#コード流れ

1. range(0, Math.min(list.size(), list2.size()))
`IntStream.range(0, 4)`  
生成される値は：0, 1, 2, 3  



■mapToObj  
`<R> Stream<R> mapToObj(IntFunction<? extends R> mapper)`  
mapToObj は「数値ストリーム（IntStream）をオブジェクトストリーム（Stream<T>）に変換するためのメソッド」。

※*list.get(i) + " " + list2.get(i)*  
という String を作る。  
