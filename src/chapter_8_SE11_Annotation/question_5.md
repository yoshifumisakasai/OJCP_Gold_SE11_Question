設問5

スーパークラスのメソッド宣言を変更したときに、サブクラスのメソッドが一致しなくなることを検知するためのアノテーションとして、正しいものを選べ（１つ）


A. @Override

B. @Deprecated


C. @SuppressWarnings


D. @FunctionalInterface



#解説  


**@Override**  
スーパークラスのメソッド宣言が変更されたとき、サブクラス側のメソッドが 「正しくオーバーライドできていない」 ことをコンパイル時に検知してくれるのが @Override です。  

*@Deprecated*  
→ 非推奨のメソッドを示す  

*@SuppressWarnings*  
→ コンパイラ警告を抑制する  

*@FunctionalInterface*  
→ 関数型インタフェース（抽象メソッド1つ）を保証するためのもの。  


#@Override が検知する典型的なケース  

```
class Parent {
    void hello() {}
}

class Child extends Parent {
    @Override
    void helloo() {}  // 親に helloo() は存在しない → コンパイルエラー
}
```
**@Override がなければ 新しいメソッドとして扱われてしまい、バグに気づけない**  



