設問8


次のプログラムをコンパイル、実行したときの結果として、正しいものを選べ（１つ）



□コード1

```
public class Sample {

 public Sample(){
  System.out.println("A");
 
 }

}

```







□コード2

```

public class Main{

 public static void main(String[] args){
 
  Sample sample = new Sample(){
  
   public Sample(){
   
    System.out.println("B");
   }
  
  
  }
 
 }

}
```


A. 「A」と表示される

B. 「B」と表示される


C. コンパイルエラーが発生する

D. 実行時に例外がスローされる




#ポイント
**コンパイルエラーが発生する理由は「匿名クラスでは コンストラクタを定義できない」**  

□コード2（匿名クラス）

```
Sample sample = new Sample(){
    public Sample(){
        System.out.println("B");
    }
};
```

**匿名クラスは「名前がない」のでコンストラクタを持てない**  
*匿名クラスには クラス名がないので、コンストラクタを定義する構文が存在しない*  

・コンストラクタ定義部：  

```
public Sample(){
    System.out.println("B");
}
```

〇Java の仕様では：  


**匿名クラス → コンストラクタを定義できない**  

**代わりに インスタンス初期化子（インスタンスイニシャライザ） { ... } を使う**    


※これならOK  

```
new Sample() {
    {
        // インスタンス初期化子（OK）
        System.out.println("B");
    }
}
```


#匿名クラスとは？
匿名クラス（anonymous class）とは “名前のないクラスをその場で定義して即インスタンス化する仕組み” のこと。  
Java が内部的にクラスを生成するが、ソースコード上ではクラス名を書かない。  


〇特徴  
・クラス名を持たない  

・new の直後にクラス本体を書く  

・その場限りの実装を作るための仕組み  

・インタフェースや抽象クラスの一時的な実装に使う  

```
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello");
    }
};
```

