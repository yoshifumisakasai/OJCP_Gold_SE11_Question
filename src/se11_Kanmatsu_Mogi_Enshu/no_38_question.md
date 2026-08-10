設問38


次のコードのうち、正しく記述されているものを選べ（2つ）


A. List<? super Number> a = new ArrayList<Integer>();


B. List<? super Float> b = new ArrayList<Double>();


C. List<? super Short> c = new ArrayList<Number>();


D. List<? extends Number> d - new ArrayList<Byte>();


E. List<? extends Number> e = new ArrayList<Object>();




#super / extends の代入ルール

〇◆ ? super T
**右辺は T または T の上位型でなければならない。**  

例：? super Number

OK：Number, Object

NG：Integer, Double（Number の下位）




〇◆ ? extends T
**右辺は T または T の下位型でなければならない。**  

例：? extends Number

OK：Number, Integer, Double, Byte

NG：Object（上位）