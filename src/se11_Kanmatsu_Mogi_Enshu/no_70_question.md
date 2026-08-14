設問70


Java SEのセキュアコーディングガイドラインに従うために、次のクラスにどのような変更をすればよいか、変更内容として正しいものを選べ（3つ）


```
public class Sample {

 String[] array;
 public Sample(String[] array){
 
  this.array = array;
 }


 public String[] getArray(){
 
  return array;
 }

}


```

A. getArrayメソッドの戻り値を戻すコードを、「return array.clone();」に変更する


B. フィールドarrayをprivate finalで修飾する


C. getArrayメソッドをsynchronizedで修飾する


D. コンストラクタをprivateにする


E. フィールドをvolatileで修飾する


F. getArrayメソッドの名前をget$Arrayに変更する


G. コンストラクタでフィールドを初期化する時、「array.clone();」の結果を代入するように変更する


#ポイント

**この問題は 「可変オブジェクト（String[]）を安全に扱うための防御的コピー（defensive copy）」 がテーマ**  



□getArrayメソッドの戻り値を array.clone() にする 
→ 正しい（防御的コピー）

*可変オブジェクトをそのまま返すと外部から内部状態を破壊できる。*  
`return array.clone();`   
⇒内部配列のコピーを返すので安全。  



□フィールド array を private final にする  
→ 正しい（**カプセル化＋不変性の強化**）  

private → 外部から直接アクセスできなくなる  
final → 参照の再代入を防ぐ（不変性の一部）  
※セキュアコーディングでは 不変性の強化は重要な原則。  




□コンストラクタで array.clone() を代入する  
→ 正しい（防御的コピー）  

コンストラクタで受け取った配列をそのまま保持すると、呼び出し側が後から配列を変更できてしまう。

`this.array = array.clone();`
とすることで 内部状態の破壊を防げる。  
