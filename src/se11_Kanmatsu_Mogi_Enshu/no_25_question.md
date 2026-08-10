設問25


次のプログラムはコンパイルエラーとなる。コンパイルエラーを解消する方法として、正しいものを選べ（１つ）


```

import java.io.Serializable;

enum Type implements Serializable {

 A(1), B(2), C(3);
 int val;

 public Type(int val){
  this.val = val;
 }

}


```


A. varフィールドをprivate finalで修飾する


B. コンストラクタのアクセス修飾子をpublicからprivateに変更する


C. valフィールドをprivateで修飾する


D. Serializableインタフェースの実装をやめる


E. Enum宣言のアクセス修飾子を「なし」からpublicに変更する



#Enumクラスのコンストラクタ制限  
Java の enum は特殊なクラスで、コンストラクタは必ず private（または package-private）でなければならない。  

理由：  

enum のインスタンスは コンパイラが自動生成する定数（A, B, C）だけ  

**開発者が new してインスタンスを作ることは許されない**  

**そのため public コンストラクタは禁止**  


※次のコードは コンパイルエラー：  

```
public Type(int val){   // ← public はダメ
    this.val = val;
}
```

