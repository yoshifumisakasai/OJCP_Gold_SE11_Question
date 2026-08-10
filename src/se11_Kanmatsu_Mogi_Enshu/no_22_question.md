設問22

次のコマンドの実行結果に関する説明として、正しいものを選べ（１つ）


`> jdeps jdkinternals C:\workspace\test\jar\lib.jar`  


A. -jdkinternalsオプションの結果をコンソールに表示するには、-summaryオプションか-verboseオプションが必要であるというエラーを表示する


B. モジュールの依存関係と、参照されるJDKの内部APIすべてのパッケージ名のリストを表示する


C. -jdkinternalsオプションにより、JDKの内部APIのクラス同士の依存関係が、jar内のすべてのクラスに付いて分析される


D. -jdkinternalsオプションにより、jar内のすべてのクラスが分析され、クラス同士の依存関係がすべて出力される




#◆ -jdkinternals オプションとは
**jdeps が JDK の内部 API（sun. / com.sun.）への依存を検出する**ためのオプション。**  

つまり：
・jar が どの内部 API を参照しているか  
・その パッケージ一覧  

を表示する。


*-jdkinternals が出すのは 内部 API のパッケージ一覧であって、クラス同士の依存関係ではない。*    
*jar 内のすべてのクラスの依存関係を出力はしません、-jdkinternals は内部 API に限定した解析を行う*  
