設問21

次のプログラムをコンパイル、実行したときの結果として、正しく記述されているものを選べ（１つ）


```

import java.util.List;
import java.util.Optional;

public class Sample {

 public static void main(String[] args) {
 
  var list = List.of("spple","banana","orange","melon");
  Optional<String> result = list.stream()
  .filter(x -> x.contains("z"))
  .reduce((i,j) -> i+ "," + j);
  result.ifPresent(System.out::print);
 }
}

```


A. 常にコンソールへの表示が実行される


B. 結果が存在しない場合、実行時にNoSuchElementExceptionが発生する


C. 結果が存在しない場合、実行時にNullPointerExceptionが発生する


D. 結果が存在しない場合、コンソールへの表示は実行されない



#Java の Optional

〇値がある → Optional.of(value)  

〇値がない → Optional.empty()  

という 2 状態を持つコンテナ。  


#実際の実装（イメージ）：

```
public final class Optional<T> {
    private static final Optional<?> EMPTY = new Optional<>(null);

    private final T value;

    private Optional(T value) {
        this.value = value;
    }

    public static <T> Optional<T> empty() {
        return (Optional<T>) EMPTY;
    }
}
```

つまり：
・value が null の Optional を EMPTY として使い回している  
 
・Optional.empty() を呼ぶとこの EMPTY インスタンスが返ってくる  

**Optional.empty() は null ではない、Optional 型のインスタンスとして存在している**  
