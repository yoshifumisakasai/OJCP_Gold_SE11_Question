設問3


アノテーションの情報をコンパイル後に残したくない。@Retentionの定義として、正しいものを選べ（１つ）

A. @Retention(RetentionPolicy.CLASS)

B. @Retention(RetentionPolicy.SOURCE)


C. @Retention(RetentionPolicy.RUNTIME)

D. @Retention



#ポイント

`@Retention(RetentionPolicy.SOURCE)`  

**「コンパイル後にアノテーション情報を残したくない」  ＝ ソースコード上だけで使われ、クラスファイルにも残らない**    
という意味になります。



`@Retention(RetentionPolicy.CLASS)`    
→ クラスファイル（.class）には残るが、実行時には参照できない。「コンパイル後に残したくない」という条件に合わない  


`@Retention(RetentionPolicy.RUNTIME)`    
→ 実行時まで保持され、リフレクションで参照可能。条件と真逆  