設問7


次のプログラムを確認し、コンパイルエラーとなるものを選びなさい（１つ）


`List<Integer> list = List.of(0,1,2,3,4);`


A. Double a = list.get(0);


B. double b = list.get(0);


C. Integer c = Integer.valueOf(list.get(0));


D. Double d = Double.valueOf(list.get(0));


E. Integer e = list.get(0);


F. int f = list.get(0);



#前提知識  

A:  
`List<Integer> list = List.of(0,1,2,3,4);`  

list.get(0) の型は Integer  
オートボクシングで int → Integer  

※詳細説明：  
list.get(0) の型が Integer になる理由は「List<Integer> と宣言した時点で、List の型パラメータ E が Integer に確定する」。    
つまり ジェネリクスの型パラメータがそのまま get の戻り値型になる。  
⇒List<Integer> と書いた瞬間、List の型パラメータ E = Integer に決まる。  

List インタフェースの get メソッド定義：  
`E get(int index);`  
E = Integer  
get(int) の戻り値は Integer 


B:  
`double b = list.get(0);`  
右辺：Integer  

左辺：double  

Integer → int（アンボクシング）

int → double（プリミティブの拡大変換）




#ボクシング（boxing）とアンボクシング（unboxing）
プリミティブ型 ↔ ラッパークラスの自動変換のこと。   
※Java が「勝手に」変換してくれる仕組みで、コレクションやジェネリクスと一緒に使うときに必須になる。  

**ボクシング：int → Integer のように、プリミティブをラッパークラスへ自動変換**
**アンボクシング：Integer → int のように、ラッパークラスをプリミティブへ自動変換**  


例）
1. コレクションはプリミティブを扱えない  

`List<int> list;` // 不可能  

`List<Integer> list = List.of(1,2,3);`  
このとき 1 は Integer にボクシングされる。  



#プリミティブの拡大変換  
「プリミティブの拡大変換（widening primitive conversion）」とは、より“広い”表現力を持つプリミティブ型へ自動的に変換されること。   
拡大変換（widening）＝情報が失われない方向への変換だから自動で許される。  


■プリミティブ型の「広さ」  
Java のプリミティブ型は「表現できる数値の範囲」が違う。  

広い順に並べる：  

`byte → short → int → long → float → double`  
※double が一番広い（表現力が高い）。



#Double.valueOf(list.get(0)) が成立する理由  
Integer → int（アンボクシング） → double（拡大変換） → Double（ボクシング）  
という 3 ステップが自動で行われる  

① list.get(0) の型は Integer
List<E> の E が Integer  



② Integer → int（アンボクシング）
Double.valueOf の引数に Integer を渡すと、Java はまずアンボクシングを行う。  

`Integer x = list.get(0);`  
int primitive = x.intValue(); // これがアンボクシング  
Java が勝手に intValue() を呼んでくれる。  


③ int → double（プリミティブの拡大変換）  
次に、Double.valueOf のオーバーロード：  

`public static Double valueOf(double d)`  
つまり double を受け取るメソッドしかない。  

Java は：  
int → double に変換する  
（これは「拡大変換」＝情報が失われないので自動でOK）  



④ double → Double（ボクシング）  
最後に、Double.valueOf(double) が呼ばれる。  


`Double d = Double.valueOf(widened);`  
これは double → Double のボクシング。  


#Integer.valuef()とDouble.valueOf()の違い

Integer.valueOf(int)   受け取る型:int、返す型:Integer  
Double.valueOf(double) 受け取る型:double、返す型:Double  
