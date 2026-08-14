設問72

次のプログラムを使った処理として、誤っているものを選べ（１つ）


```
List<String> data = List.of("apple", "banana", "orange");
List<String> backup = new ArrayList<>();

```


A. data.parallelStream()
   .filter(str -> str.indexOf('n') != -1)
   .forEach(str -> backup.add(str));
   
 

B. data.stream()
   .filter(str -> str.indexOf('n') != -1)
   .parallel()
   .collect(backup);   
   

C. data.stream()
   .filter(str -> str.indexOf('n') != -1)
   .parallel()
   .forEach(str -> backup.add(str));
   
   

D. backup = data.stream()
   .filter(str -> str.indexOf('n') != -1)
   .parallel()
   .forEach(Collectors.toList());
   
   
   
   
   
   
   
   
-------------------------

#選択肢判定


❌ D.

```
backup = data.stream()
    .filter(str -> str.indexOf('n') != -1)
    .parallel()
    .forEach(Collectors.toList());
```
❌ forEach は 戻り値が void  
forEach の戻り値は void なので、backup = ... の右辺に置くことは コンパイルエラー。  

（観点）  
※forEach は Consumer<? super T> を受け取る。  
しかし Collectors.toList() は Collector であり、型が全く違う。  





B.

```
data.stream()
    .filter(str -> str.indexOf('n') != -1)
    .parallel()
    .collect(backup);
```

✔ collect の第1引数は Collector  
※Collector は「Stream の終端処理をどう集約するかを定義する“収集器”インタフェース」　　
collect(backup) は コンパイルエラーではない    
（raw type の collect(Object) が呼ばれる）  