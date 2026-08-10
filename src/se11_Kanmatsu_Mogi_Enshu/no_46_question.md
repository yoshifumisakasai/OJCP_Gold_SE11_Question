設問46


数値のリストの平均を求めるコードとして、正しいものを選べ（１つ）


A. double a = list.stream()
   .collect(Collectors.averagingDouble(n -> n));
   
   
B. double a = list.parallelStream()
   .mapToInt(m -> m).average().getAsDouble();
   
   
C. double a = list.stream()
   .average().getAsDouble();
   
   
D. double a = list.stream()
   .parallel().averagingDouble(n -> n);
   
   
E. double a = list.stream()
   .mapToInt(n -> n).average().parallel();





#選択肢判定

A. double a = list.stream().collect(Collectors.averagingDouble(n -> n));
✔ 正しい

averagingDouble は平均値を double で返す Collector

n -> n は Integer を double に自動変換（オートアンボクシング＋数値変換）

戻り値は double

平均値を求める処理として正しい



B. double a = list.parallelStream().mapToInt(m -> m).average().getAsDouble();
✔ これも平均値は求まるが…

試験問題では 「正しいものを選べ（1つ）」  
→ 最も標準的で意図に合うのは A。

ただし B も動く。
しかし parallelStream を使う理由がないため、試験では不正扱い。



C. list.stream().average().getAsDouble();
❌ コンパイルエラー

**average() は IntStream / LongStream / DoubleStream にしか存在しない。**  

list.stream() は Stream<Integer>  
`→ average() は存在しない`
→ コンパイルエラー




D. list.stream().parallel().averagingDouble(n -> n);

**❌ averagingDouble は Stream のメソッドではない**  

```
averagingDouble は Collectors のメソッド  
Stream に直接 averagingDouble は存在しない
```

→ コンパイルエラー




E. list.stream().mapToInt(n -> n).average().parallel();

```
❌ parallel() は OptionalDouble に存在しない
average() の戻り値は OptionalDouble  、OptionalDouble に parallel() はない
```
→ コンパイルエラー

Java の Stream API ：

✔ Stream にあるメソッド  
parallel()  
**parallel() は ストリームの処理を並列化するための指示**  

-------------------------------

#collectメソッドと、Collectorsクラス
collectメソッドは「Stream の終端操作で、結果を 1 つのオブジェクトに“集約”するためのメソッド」  
Collectors クラスは「collect に渡すための Collector（収集器）を作る“工場”」。



■要点  

collect()：Stream の終端操作。Collector を使って結果をまとめる。

Collector：集約処理のルール（どう集めるか）を定義するインタフェース。

Collectors：よく使う Collector を作るためのユーティリティクラス。




---------------------------------

■対象コード  

```
double a = list.stream()
   .collect(Collectors.averagingDouble(n -> n));
```
   
◆ 1. collectメソッドとは何か（Stream の終端操作）

Stream の要素を 1 つの結果にまとめる（集約する）ためのメソッド。

✔ シグネチャ
`<R, A> R collect(Collector<? super T, A, R> collector)`  
✔ 型パラメータの意味
T：Stream の要素型

A：中間バッファ（蓄積用オブジェクト）

R：最終的な戻り値の型

✔ collect の動作
Collector が持つ 4 つの関数を使って Stream の要素を集約する：

supplier：中間バッファを作る

accumulator：要素をバッファに追加

combiner：並列処理時にバッファを結合

finisher：最終結果に変換

collect はこれらを順番に呼び出して結果を作る。




◆ 2. Collector とは何か（集約処理のルール）
Collector は「どう集めるか」を定義するインタフェース。

✔ 例：toList() の Collector のイメージ


supplier:   () -> new ArrayList<>()
accumulator: (list, elem) -> list.add(elem)
combiner:   (list1, list2) -> { list1.addAll(list2); return list1; }
finisher:   list -> list
collect はこれを使って Stream の要素を List にまとめる。




◆ 3. Collectors クラスとは何か（Collector を作る工場）
Collectors は Collector を簡単に作るための静的メソッド集。

✔ 代表的なメソッド
toList() → List に集約

toSet() → Set に集約

joining() → 文字列連結

groupingBy() → グループ化

averagingDouble() → 平均値

summingInt() → 合計値

counting() → 件数

Collectors は「よく使う Collector」を全部用意してくれている。

◆ 4. collect と Collectors の関係（芳文の例で説明）
芳文のコード：

java
double a = list.stream()
    .collect(Collectors.averagingDouble(n -> n));
✔ 何が起きているか
averagingDouble(n -> n) が Collector<Double> を作る

collect がその Collector を使って

sum

count
を内部バッファに保持

最後に sum / count を返す

結果は Double（平均値）

つまり：

コード
collect(averagingDouble) = 平均値を計算する終端操作
◆ 5. collect の本質（芳文向けに内部仕様まで）
collect は Stream の終端操作であり、
reduce の一般化とも言われる。

reduce は「1つの値に畳み込む」だけだが、
collect は：

中間バッファを持てる

並列処理に強い

複雑な集約（グループ化・統計・結合）ができる

という強力な仕組み。

◆ 6. 芳文向けの最終まとめ
✔ collect
Stream の終端操作

Collector を使って結果を 1 つにまとめる

reduce の上位互換

✔ Collector
集約処理のルール

supplier / accumulator / combiner / finisher を持つ

✔ Collectors
Collector を作るユーティリティ

toList, groupingBy, averagingDouble など便利メソッド多数