設問3

次のクラスをインスタンス化するためのコードとして、ためのコードとして、正しいものを選べ（１つ）



```
public class Outer {

 public static class Inner {
 
  // do something
 }

}


```

A. Inner inner = new Inner();


B. Inner inner = new Outer().new Inner();


C. Inner inner = Outer.new Inner();


D. Inner inner = new Outer().Inner();




#ポイント
**static インナークラスなので、前の問題（非 static インナークラス）とはルールが完全に逆になる**  

**static インナークラスは「Outer に紐づかない」**  

```
・Outer のインスタンスは不要  

・単独で new できる  

・外側クラスの this を必要としない  
```



