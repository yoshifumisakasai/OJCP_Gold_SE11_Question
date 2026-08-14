設問55

次のプログラムの実行結果として、「2021年 4月 1日 木曜日」と表示したい。
以下の「insert code here」に入るコードとして、正しいものを選べ（１つ）


```
LocalDate date = LocalDate.of(2021, 4, 1);
DateTimeFormatter formatter = DateTimeFormatter.ofPattern(/* insert code here*/);
System.out.println(formatter.format(date));

```


A. "yyyy"+年 + "MMM dd+"日"+eeee"


B. "yyyy"+年 + "MMMM d+"日"+eeee"


C. "yyyy'年' MMMM d'日' eeee"


D. "yyyy'年' MMM dd'日' eeee"




#1. DateTimeFormatter.ofPattern の書式ルール
yyyy → 西暦4桁

'年' → リテラル文字列「年」

MMMM → 月のフルスペル（例：April）

d → 日（1桁でもOK）

'日' → リテラル文字列「日」

eeee → 曜日（フルスペル）


#選択肢の切り分け
A. "yyyy"+年 + "MMM dd+"日"+eeee"  
❌ "+" は文字列連結ではなく、パターン文字列としては不正 → コンパイルエラー



B. "yyyy"+年 + "MMMM d+"日"+eeee"  
❌ 同上、"+" は不正



C. "yyyy'年' MMMM d'日' eeee"  
⭕ 正しい。リテラル部分を ' ' で囲んでいる



D. "yyyy'年' MMM dd'日' eeee"  
❌ dd は「ゼロ埋め2桁」なので「01日」となる → 問題文の「1日」とは異なる