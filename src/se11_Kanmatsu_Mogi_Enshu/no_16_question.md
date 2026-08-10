設問16


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


```

import java.util.Arrays;
public class Sample {

 private String name;
 private int num;

public Sample(String name, int num){

 this.name = name;
 this.num = num;
}

public int getNum(){

 return this.num;
}

public static void main(String[] args){

 var samples = Arrays.asList(
         new Sample("A", 8),
         new Sample("B", 21),
         new Sample("C", 23),
         new Sample("D", 12)
         );
         
         
 int result = samples.stream()
            .mapToInt(Sample::getNum)
            .filter(s -> s < 20)
            .reduce(0, (a,b) -> a + b);
 System.out.println(result);
}

}

```



A. 「44」と表示される


B. 「20」と表示される


C. 「35」と表示される


D. 「29」と表示される


E. コンパイルエラーが発生する
