設問12


次のプログラムの変数numをスレッドセーフにするための修正方法として、正しいものを選べ（2つ）


```
public class Sample{

 private int num = 0;
 public static void main(String[] args){
 
  Sample s = new Sample();
  ExecutorService service = Executors.newFixedThreadPool(10);
  
  for(int i = 0; i<10; i++){
   service.submit()) -> {
    for(int j = 0; j < 100000; j++){
    
     s.sum++;//line
    }
   
   });
  
  
  }
 service.shutdown();
 }

}

```


A. mainメソッドのメソッド宣言にsynchronizedを追加する


B. lineの位置コードを、次のコードに置き換える
synchronized(s){
 s.num++;
 }
 
 
C. lineの位置コードを、次のコードに置き換える
synchronized(s.num){
 s.num++;
 }

D. numフィールドのフィールド宣言にvolatileを追加する


E. numフィールドのデータ型をAtomicIntegerに置き換え、lineの位置コードを、次のコードに置き換える
s.num.incrementAndGet();



#ポイント
**「num++ が非原子的（atomic ではない）であり、複数スレッドから同時に実行されると競合が発生するため、排他制御か Atomic クラスが必要**


#前提：なぜ num++ はスレッドセーフではないのか？
num++ は以下の 3 ステップに分解される：  

(1) num を読み取る  

(2) 1 を加算する  

(3) num に書き戻す  

**これらが atomic（不可分）ではないため、複数スレッドが同時に実行すると値が失われる（race condition）**  







■選択肢判定：

----------------------------------------------


B. synchronized(s) { s.num++; }  

```
synchronized(s) {
    s.num++;
}
```
**s をロックオブジェクトとして排他制御するため、複数スレッドが同時に num++ を実行できなくなる。**  


E. AtomicInteger に変更し、incrementAndGet() を使う

```
private AtomicInteger num = new AtomicInteger(0);
s.num.incrementAndGet();
```

**AtomicInteger の incrementAndGet() は atomic（原子的） に実行される。複数スレッドから同時に呼ばれても安全。**  






■選択肢判定2：

----------------------------------------------




D. num に volatile を付ける  
`private volatile int num;`  
❌ 不正解
**volatile は「可視性の保証」だけであり、atomic（原子性）は保証しない。**
つまり num++ の競合は防げない。  






A. main メソッドに synchronized を付ける
`public synchronized static void main(String[] args)`  
❌ 不正解
**main を synchronized にしても 複数スレッドが同時に num++ を実行する状況は変わらない。**
synchronized は「メソッドを呼ぶスレッドを排他する」だけであり、内部で生成した ExecutorService のスレッドには影響しない。  

