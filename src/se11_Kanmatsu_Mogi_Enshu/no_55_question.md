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