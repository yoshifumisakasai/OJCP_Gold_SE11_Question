設問23

次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


```
import java.util.stream.IntStream;
import java.util.stream.Stream;


public class Sample {

 public static void main(String[] args){
 
  int array[][] = {{1,2},{3,4},{5,6}};
  long count = Stream.of(array)
  .flatMapToInt(IntStream::of)
  .map(n -> n * 2)
  .peek(System.out::print)
  .filter(n -> (n % 3 == 0))
  .count();
  System.out.println(" " + count);
 
 }

}
```


A. 「2」と表示される


B. 「24681012 2」と表示される


C. 「2610 2」と表示される


D. 「4812 2」と表示される


E. コンパイルエラーが発生する


