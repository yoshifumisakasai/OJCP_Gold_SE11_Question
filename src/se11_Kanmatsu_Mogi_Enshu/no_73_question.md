設問73


次のコードのうち、正しく記述されているものを選べ（１つ）



A. Function<int> a = n -> n * 2;


B. Function<int, int> c = n -> n * 2;


C. Function<Integer, Integer> b = n -> n * 2;


D. Function<Integer> d = n -> n * 2;


E. Function e = n -> n * 2;



#ポイント 

*Function<T, R> は T を受け取り R を返す関数型インタフェース。*  

入力：Integer

出力：Integer

ラムダ：n -> n * 2（戻り値は int → Integer にボックス化）  
