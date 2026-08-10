設問1

アノテーションの定義として、正しいものを選べ（１つ）

A. public @interface Sample {}


B. public interface Sample {}


C. public @annotation Sample {}


D. public annotation Sample {}



#ポイント
Javaでアノテーションを定義する場合、必ず @interface を使うという仕様になっています。
通常のインタフェースは interface ですが、アノテーション専用の構文として @interface が用意されています。


■アノテーション定義の基本形

```
public @interface Sample {
    String value();
}
```
