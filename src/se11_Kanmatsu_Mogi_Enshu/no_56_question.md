設問56

次のプログラムを確認してください


□コード1

```
public enum Type {

 A(1), B(2), C(3);
 int val;
 private Type(int val){
  this.val = val;
 }

}

```



以下の「insert code here」に入るコードとして、正しいものを選べ（１つ）


□コード2

```
public class Sample {

 public static void main(String[] args){
 
  Type type = Type.A;
  
  
  switch(type){
  
   case /* insert code here*/ :
    System.out.println("A");
    break;
   
   default:
    System.out.println("B");
    break;
  
  }
 }

}

```


A. Type.A.valueOf()


B. A


C. Type.A


D. A.toString()



#コード解説
🎯 1. enum は特殊なクラス（Type はクラス）  
Java の enum は、コンパイラが自動的にクラスとして展開する特殊な構文。  

■内部的なクラスのイメージ：

```
public final class Type extends Enum<Type> {
    public static final Type A = new Type(1);
    public static final Type B = new Type(2);
    public static final Type C = new Type(3);

    private final int val;

    private Type(int val) {
        this.val = val;
    }
}
```

つまり：

A, B, C は Type の唯一のインスタンス

それぞれ val に 1, 2, 3 を持つ

🎯 2. A(1), B(2), C(3) はコンストラクタ呼び出し
A(1) は Type のコンストラクタに 1 を渡している。

つまり：

A → new Type(1)

B → new Type(2)

C → new Type(3)

ただし、enum は 開発者が new できない  
→ コンパイラが自動的に new してくれる。

🎯 3. コンストラクタは private でなければならない
java
private Type(int val)
enum のコンストラクタは 必ず private（または package-private）。

理由：

enum のインスタンスは コンパイラが生成する定数だけ

開発者が new して増やすことは許されない

🎯 4. フィールド val は各定数が持つ値
java
int val;
A.val = 1

B.val = 2

C.val = 3

このように、enum の各定数は 固有の値を持てる。

🎯 5. enum の内部は実は「シングルトンの集合」
各定数は 唯一のインスタンス。

Type.A == Type.A は true

Type.A.equals(Type.A) も true

Type.A は JVM 内に 1 個しか存在しない

🎯 6. 暗黙的に生成されるメソッド
enum にはコンパイラが自動生成するメソッドがある：

values()
java
Type[] arr = Type.values();
→ [A, B, C] の配列を返す
→ 宣言順に並ぶ

valueOf(String)
java
Type t = Type.valueOf("A");
→ 文字列から enum を取得

✔ まとめ（芳文向けに要点だけ）
enum Type は Type クラスとして展開される

A(1) は コンストラクタ呼び出しで、val = 1 を持つ

コンストラクタは private（enum の仕様）

A, B, C は 唯一のインスタンス（シングルトン）

values() は 宣言順の配列を返す