設問58

Systemクラスに関する説明として、正しいものを選べ（１つ）


A. System.inは、標準入力ストリームである。個のストリームは常に開いている


B. System.inにほかのストリームを置き換えることはできない


C. デフォルトでは、System.outはjava.io.OutputStreamのインスタンスである


D. System.outは標準出力ストリームである。このストリームは、System.outを呼び出した場合のみ開く



#System.in
 
**常に開いている標準入力ストリーム**  


■System.inとは？
・System.in は JVM 起動時に OS の 標準入力（stdin） に接続される  

・JVM が終了するまで 閉じられない（常に開いている）  

・close() を呼ぶことはできるが、通常は閉じない前提で設計されている  



■System.outとは？  
System.outは標準出力ストリームである。このストリームは、起動時にすでに開いている  

（特徴）  
・JVM 起動時に OS の stdout に接続される  

・System.out.println() を呼ぶ前から 常に開いている  

※System.out は PrintStream  
*PrintStream は OutputStream を内部に持つが、System.out 自体は OutputStream ではない。*  


#置き換えについて
System.setIn(InputStream in) により、標準入力を任意のストリームに差し替えられる。
「標準入力（System.in）を、別の InputStream に差し替えて使える」という意味  
キーボード入力の代わりに、ファイルやメモリ上のデータを標準入力として扱えるということ。  
**通常、System.in は OS の 標準入力（stdin） に接続されていて、キーボードからの入力を読み取る。**  

★「System.setIn(InputStream in)」を使うことで、System.in を任意の InputStream に置き換えることができる。  




■具体例1：キーボード入力の代わりにファイルを使う

```
System.setIn(new FileInputStream("input.txt"));  
Scanner sc = new Scanner(System.in);  
```
Scanner(System.in) は キーボードではなく input.txt を読む  



■具体例2：テストでよく使う「擬似入力」  

```
String fakeInput = "hello\nworld\n";  
System.setIn(new ByteArrayInputStream(fakeInput.getBytes()));  

Scanner sc = new Scanner(System.in);  
System.out.println(sc.nextLine()); // hello  
System.out.println(sc.nextLine()); // world  
```

・テストコードで「標準入力を模擬」できる  
 
・キーボードを使わずに入力を再現できる  


例：  
`System.setIn(new FileInputStream("input.txt"));`  
