設問76


readObjectメソッドが呼び出されるタイミングとして、正しいものを選べ（１つ）


```
import java.io.ObjectInputStream;
import java.io.Serializable;


public class Sample implements Serializable {

 private String value;
 
 public Sample(String value){
 
  this.value = value;
 }
 
 private void readObject(ObjectInputStream in){
 
  try [
   in.defaultReadObject();
  }catch (Exception e9 {
  
   throw new RuntimeException();
  }
 }
}


```


A. このオブジェクトのデシリアライズ後


B. このオブジェクトのシリアライズ後


C. このオブジェクトのデシリアライズ前


D. このオブジェクトのシリアライズ前


E. 呼び出されることはない




#readObject  
readObject(ObjectInputStream in) は デシリアライズの過程で呼ばれる特別メソッド。
オブジェクトが復元される直前（デシリアライズの途中）で呼ばれる。  
`private void readObject(ObjectInputStream in)　throws IOException, ClassNotFoundException`  


■【readObject のシグネチャ】  

✔ 必ず private  
public や protected にすると 特別メソッドとして扱われない

※Java のシリアライズ機構は private を反射で呼び出す  


✔ 戻り値は void 

「Employee を返す」と誤解して (Employee) in.readObject() と書く人が多い

readObject は 戻り値なし（void）  
✔ 引数は ObjectInputStream  


✔ throws IOException, ClassNotFoundException、IOException は必須  
ClassNotFoundException は “defaultReadObject が投げる可能性があるため” 必要  


#writeObject  
writeObject は「オブジェクトをシリアライズする直前に呼ばれる“カスタムシリアライズ処理”のための特別メソッド」。
(シリアライズ時に自動的に呼び出される特別メソッド)   
`private void writeObject(ObjectOutputStream out) throws IOException`  


■【writeObject のシグネチャ】     

・private でなければならない（public だと特別メソッドとして扱われない）   

・戻り値は void  

・引数は ObjectOutputStream  

・throws IOException が必要  