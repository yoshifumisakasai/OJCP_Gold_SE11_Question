設問44

以下の「insert code here」に入るコードとして、正しいものを選べ（１つ）

```
List<Integer> list = Arrays.asList(1,2,3,4,5);
UnaryOperator<Integer> op = /* insert code here */;
list.replaceAll(op);
list.stream().forEach(System.out::println);

```


A. a, b -> a * b


B. (int a) -> a * 2


C. var a -> a * 2


D. a -> a

#ポイント
UnaryOperator<T> は 「T を受け取り T を返す関数」。  
そのため、正しいラムダ式は 引数 1つ → 戻り値も同じ型 の形  
