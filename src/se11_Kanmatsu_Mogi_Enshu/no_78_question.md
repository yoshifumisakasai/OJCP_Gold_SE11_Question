設問78


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）


```
import java.util.List;
import java.util.function.Consumer;


public class Sample {

 public static void main(String[] args){
 
  List<String> list = List.of("A", "B", "C");
  Consumer<String> a = System.out::print;
  Consumer<String> b = 
  a.andThen(
  str -> System.out.println(":" + str.toLowerCase())
  );
  list.forEach(b);
 }

}

```


A. 「:a:b:c」「ABC」と表示される


B. 「a:A」「b:B」「c:C」と表示される


C. 「ABC」「:a:b:c」と表示される


D. 「:a:b:c」と表示される


E. 「A:a」「B:b」「C:c」と表示される



#🎯 なぜ C（「ABC」「:a:b:c」）に見えてしまうのか？
あなたの頭の中ではこう動いたはず：

System.out::print が先に実行される
→ "A" "B" "C" が連続で出る
→ "ABC" に見える

次に println(":" + str.toLowerCase()) が実行される
→ ":a" ":b" ":c" が出る
→ ":a:b:c" に見える

つまり print の連続 → println の連続 と誤解してしまう。

しかし実際は、
**要素ごとに andThen が実行される**  



