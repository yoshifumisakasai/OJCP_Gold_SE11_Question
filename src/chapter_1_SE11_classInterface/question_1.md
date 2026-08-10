設問1


次の説明のうち、正しいものを選べ（１つ）


A. インナークラスはprivateで修飾できない


B. staticなインナークラスはpublicで修飾できない


C. ローカルクラスはpublicで修飾できない


D. 匿名クラスはfinalで修飾できない



#理解ポイント1
**インナークラス（非 static / static どちらも）は、private / protected / public / default いずれでも修飾できる**  

```
public class Outer {
    private class Inner { }
}
```

#理解ポイント2
**static ネストクラスも public にできる**

```
public class Outer {
    public static class Inner { }
}
```

#理解ポイント3
**匿名クラスは「クラス名がない」ため、修飾子を付けるという概念自体が存在しない**  


#理解ポイント4
**ローカルクラスはメソッド内で宣言されるため、アクセス修飾子（public / private / protected）は付けられない**  
**付けられるのは final / abstract などの非アクセス修飾子のみ**  



#インナークラス・ローカルクラス・匿名クラスの違い


■ **1. インナークラス（メンバークラス）**  
✔ 特徴
クラスのメンバーとして宣言されるクラス

static / non-static の2種類がある

アクセス修飾子を自由に使える
→ public / protected / private / default

✔ 例

```
public class Outer {
    private class Inner { }
    public static class StaticInner { }
}
```

✔ JVMでの実体
Outer$Inner.class

Outer$StaticInner.class

✔ 使いどころ
外側クラスと密接に関連する補助的なクラス

外側のフィールドにアクセスしたい場合（非 static インナークラス）





■ **2. ローカルクラス（メソッド内クラス）**  
✔ 特徴
メソッド内で宣言されるクラス

アクセス修飾子（public/private/protected）は付けられない

付けられるのは final / abstract などの非アクセス修飾子のみ

メソッド外からは参照できない

✔ 例

```
void method() {
    class Local {
        void run() {}
    }
    Local l = new Local();
    l.run();
}
```

✔ JVMでの実体
Outer$1Local.class のような名前で生成される

✔ 使いどころ
メソッド内だけで使う小さな補助クラス

変数キャプチャ（実質 final）と相性が良い




■ **3. 匿名クラス（anonymous class）**  
✔ 特徴
クラス名がない

new の直後に { ... } でクラス本体を書く

修飾子を付けるという概念自体が存在しない

1回限りの実装に使う


✔ 例

```
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello");
    }
};
```

✔ JVMでの実体
Outer$1.class のような番号付きクラスが生成される

✔ 使いどころ
一時的なインタフェース実装

Java 8 以降はラムダ式に置き換えられる場面が多い