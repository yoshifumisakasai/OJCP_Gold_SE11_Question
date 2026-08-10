設問2


次のコードのうち、ファイルの読み込み後にStreamオブジェクトを取得できるものを選びなさい（１つ）


A. var a = Files.lines(Paths.get(fileName));


B. var b = Files.readAllLines(Paths.get(fileName));


C. Stream<String> c = Files.lines(fileName);


D. Stream<String> d = readAllLines(Paths.get(fileName));




#Streamを戻すメソッド(クラスFiles)

※Java の Files クラスで Stream を返すメソッドは lines() のみです。  


■「ファイル読み込み後に Stream オブジェクトを取得できる」  ＝ 戻り値が Stream<String> であるもの  
↓↓  

`public static Stream<String> lines(Path path, Charset cs) throws IOException`  
                            
`public static Stream<String> lines(Path path)　throws IOException`  

