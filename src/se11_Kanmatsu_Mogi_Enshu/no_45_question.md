設問45

10個の乱数を出力するコードとして、正しいものを選べ（１つ）



A. IntStream.generate(Random.nextInt)
   .limit(10)
   .forEach(System.out::println);


B. var r = new Random();
   IntStream.generate(r::nextInt)
   .limit(10)
   .forEach(System.out::println);
   
   

C. IntStream.generate(Random::nextInt)
   .limit(10)
   .forEach(System.out::println);
   
   
   

D. var r = new Random();
   new IntStream.generate(r::nextInt)
   .limit(10)
   .forEach(System.out::println);


#選択肢判定   

-----------------
C. IntStream.generate(Random::nextInt)
❌ コンパイルエラー

**Random::nextInt は インスタンスメソッド参照なので、クラス名から参照することはできない。**  

Random::nextInt は「Random インスタンスを引数に取る関数」として扱われるため
IntSupplier に一致しない。



A. IntStream.generate(Random.nextInt)
❌ コンパイルエラー

**Random.nextInt は インスタンスメソッド。クラス名から直接参照できない。**  
必要なのは インスタンスメソッド参照：  




D. new IntStream.generate(r::nextInt)
❌ 構文エラー

**IntStream.generate は static メソッド。new を付ける意味がないし、文法的に不正。**  








------------------------------

**B. var r = new Random();
IntStream.generate(r::nextInt) …**
✔ 正しい

`IntStream.generate は IntSupplier を要求する。`  

r::nextInt は Random インスタンスの nextInt() を呼び出す

```
→ int getAsInt() と互換
→ IntSupplier として使える
```

↓↓↓↓↓↓↓↓↓↓

IntStream.generate(r::nextInt) が使える理由：

Random#nextInt() のシグネチャが IntSupplier の抽象メソッドと一致している。


---------------------------------------------------

#IntSupplier とメソッド参照の互換性  

■① IntStream.generateの仕様チェック

  static IntStream generate(IntSupplier s)
  ※指定されたIntSupplierによって生成される要素を含む、順序付けされていない無限順次ストリームを返します。 

  □パラメータ:
  s - 要素を生成するためのIntSupplier   

  □戻り値: 
  順序付けされていない新しい無限順次IntStream  



■② r::nextIntの仕様チェック

※2種類（オーバーライド）  
public int nextInt(int bound)  
public int nextInt()  

引数なし
戻り値型：int



---------------------------------------------------

※IntStream.generateの引数にセットしているインタフェース：　　
■Java の関数型インタフェース IntSupplier 定義：

```
@FunctionalInterface
public interface IntSupplier {
    int getAsInt();
```

・引数なし
・戻り値は int
という 関数を1つだけ持つインタフェース。  
---------------------------------------------------





〇Java 判断：　　
「r::nextInt は int getAsInt() と同じ形だから、IntSupplier として使える」

⇒これが 互換性。  


**ラムダ式やメソッド参照は、抽象メソッドの形に一致していれば、そのインタフェースとして扱える。**

`IntSupplier s = r::nextInt;`  
は OK。



#逆に一致しない例
❌ Random::nextInt（クラス名から参照）
これは「Random を引数に取る関数」として扱われる。

つまり：
`Random::nextInt`  
⇒IntSupplier ではなく  Function<Random, Integer> のような形になる。
※generate に渡せない。



#「r::nextInt」記票について
r::nextInt は「Random インスタンス r の nextInt() メソッドを “関数として渡す”」ための記法であって、
“ただ nextInt() を呼んでいる” のとは全く違う。

■r.nextInt()
・今すぐ nextInt() を呼ぶ

■r::nextInt
・nextInt() を呼び出す “関数” を渡す →「乱数を返す処理を “関数として” 渡すから、必要になったら呼んで使う」



r::nextInt を匿名クラスで書く：

```
IntSupplier s = new IntSupplier() {
    @Override
    public int getAsInt() {
        return r.nextInt();
    }
```

r::nextInt をラムダ式で書く：  
() -> r.nextInt()  

※左辺も書くと下記  
IntSupplier s = () -> r.nextInt();  
