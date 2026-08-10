設問2


独自に定義するアノテーションにString型の注釈パラメータ「test」を宣言したい。正しい記述を選べ（１つ）


A. String test;


B. void test (String value);


C. String test();


D. @test


#ポイント

アノテーションの要素（＝注釈パラメータ）は、
「戻り値の型を持つ抽象メソッド」として宣言する、というのが Java の仕様です。



**アノテーション要素は「引数なし・戻り値あり」の形のみ**  
**アノテーションはフィールドを持てない**  


〇アノテーション要素の例

```
public @interface Sample {
    String test();        // 要素
    int value() default 1; // default値も付けられる
}
```


■アノテーション要素は以下の型のみ使用可能  

・プリミティブ型  
・String  
・Class  
・enum  
・他のアノテーション  
・上記の配列  