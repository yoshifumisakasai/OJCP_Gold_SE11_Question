設問79


次のプログラムの「insert code here」に記述するHelloクラスのインスタンスを生成するコードとして、正しいものを選べ（１つ）


```
public class Sample {

 class Hello {
 
  // some code
 }
 
 public static void main(String[] args){
 
  // insert code here
 }

}


```



A. Sample a = new Sample();
   Hello h = new Hello();
   
   
   
   
B. Sample b = new Sample();
   Sample.Hello h = b.new Hello();
   
   
   
   
C. Sample c = new Sample();
   Sample.Hello h = c.new Sample.Hello();
   
   
   
   
D. Sample.Hello d = new Sample.Hello();





#非 static なメンバークラス（インナークラス）のインスタンス化

□インナークラス（非 static）の原則
`class Hello { ... }`  
これは Sample のインスタンスに紐づくインナークラス。  

※Hello を new するには、まず Sample のインスタンスが必要。  




------------------

D. Sample.Hello d = new Sample.Hello();

`Sample.Hello d = new Sample.Hello();`  
❌ 非 static インナークラスは 外側インスタンスなしでは new できない。new Sampleしていると思いますが、何か問題ですか？new Sampleに対して、メソッドチェインで、Helloを呼んでいるように思います。


#インナークラスの「new の構文ルール」がポイント

new Sample.Hello() は “外側インスタンスを作っている” ように見えるが、実際には Sample のインスタンスは作られていない。  



■なぜ new Sample.Hello() はダメなのか?  
✔ 非 static インナークラスは「外側インスタンスに紐づく」

```
class Sample {
    class Hello { }
}
```

この Hello は Sample のインスタンスに属するオブジェクト。

つまり内部的には：

`Hello(Sample this$0)`  
というコンストラクタを持つ。
Hello を new するには、必ず Sample のインスタンス（this$0）が必要。  





■new Sample.Hello() はどう解釈されるのか？
あなたはこう思ったはず：

「new Sample.Hello() は new Sample() に対して Hello を呼んでいるのでは？」

しかし Java の構文は そう解釈しない。

❌ new Sample.Hello() は
「Sample の static なネストクラス Hello を new する構文」

として扱われる。

つまり Java は：

Sample.Hello が static であることを前提にした構文
↓↓↓
**🎯 問題の本質：static である必要があるのは “Hello クラス” のほうです**
**✔ Sample が static である必要はない**  
**（トップレベルクラスは static になれない）**  


非 static の場合は コンパイルエラー  



■正しい構文は「外側インスタンス.new 内側クラス」

```
Sample outer = new Sample();
Sample.Hello inner = outer.new Hello();
```
この形だけが正しい。
