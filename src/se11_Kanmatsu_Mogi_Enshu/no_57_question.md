設問57

デフォルトのロケールを設定するコードとして、正しいものを選べ（2つ）


A. Locale.setDefault(Locale.Category.FORMAT, Locale.JAPANESE);


B. Locale.setDefault("es", Locale.US);


C. Locale.setDefault(Locale.JAPANESE);


D. Locale.setDefault(Locale.Category.FORMAT, "ja_JP");


E. Locale.setDefault("ja_JP");




#Locale.setDefault には 2 種類のオーバーロード：  

全体のデフォルトロケールを設定する  
`public static void setDefault(Locale newLocale)`  


カテゴリごとのデフォルトロケールを設定する  
`public static void setDefault(Locale.Category category, Locale newLocale)`    

