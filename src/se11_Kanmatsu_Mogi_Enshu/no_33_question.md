設問33


次のプログラムに関する説明として、正しいものを選べ（１つ）


□コード1

```
public class Test{

 public synchronized void execute (Sample... samples){
 
  for(int i = 0; i < 10; i++){
  
   while (!samples[0].hello(this)){
    // do something
   }
   
   while (!samples[1].hello(this)){
   
    // do something
   }
   
   samples[1].bye();
   samples[0].bye();
  
  }
 
 }

}

```


□コード2

```
public class Sample {

 public Test test;
 public synchronized boolean hello ( Test test){
 
  if(this.test == null){
  
   this.test = test;
   return true;
  }
  return false;
 }
 
 public synchronized void bye(){
 
  test = null;
 }

}

```


□コード3

```
public class Main{

 public static void main(String[] args){
 
  Test t1 = new Test();
  Test t2 = new Test();
  
  Sample s1 = new Sample();
  Sample s2 = new Sample();
  
  new Thread(() ->{
  
   t1.execute(s1,s2);
  
  }).start();
  
  new Thread(() ->{
  
   t2.execute(s1,s2);
  
  }).start();
  
 }
}

```


A. デッドロックの可能性がある


B. ライブロックの可能性がある


C. IllegalMonitorStateExceptionがスローされる


D. コンパイルエラーとなる


# 同期メソッド同士が互いのロックを奪い合うかどうか


■Thread-1（t1.execute）
t1 のロック取得

□(解説）  
**Thread‑1 が t1.execute(...) を呼ぶと、t1 インスタンスのモニターロック（排他ロック）を取得する。**  
**◆ synchronized メソッドは「そのメソッドを持つインスタンスのロック」を取る**  
**synchronized が付いている instance メソッドは、メソッドを呼び出した インスタンスのモニター（monitor） をロックする**
つまり this のロックを取る

s1.hello(this) → s1 のロック取得

s2.hello(this) → s2 のロック取得

□(解説）  
synchronized が付いた インスタンスメソッドは、
内部的にはこう扱われる：

```
public boolean hello(Test test) {
    synchronized(this) {   // ← this は s1
        ...
    }
}
```
つまり：
s1.hello(this) は “s1 インスタンスのロックを取得する”。  
s1.hello(...) → synchronized(s1)   

s2.hello(this) は “s2 インスタンスのロックを取得する”。  
s2.hello(...) → synchronized(s2)  



■Thread-2（t2.execute）
t2 のロック取得

s1.hello(this) → s1 のロック取得

s2.hello(this) → s2 のロック取得


#デッドロックが起きる典型パターン

ある瞬間：
Thread-1 が s1 のロックを保持

Thread-2 が s2 のロックを保持

そして両者は次のロックを待つ：

Thread-1 は s2 のロックを待つ

Thread-2 は s1 のロックを待つ


つまり：
Thread-1: s1 → s2 を待つ
Thread-2: s2 → s1 を待つ
これは 完全にデッドロックの典型パターン。


#なぜ hello() がデッドロックを引き起こすのか？
hello() は synchronized なので、Sample インスタンスごとに排他ロックがかかる。  

さらに execute() 内：

while (!samples[0].hello(this)) { ... }
while (!samples[1].hello(this)) { ... }
つまり s1 → s2 の順でロックを取りに行く。

しかし別スレッドは同じ順番で取りに行くが、タイミングによって 片方が s1、もう片方が s2 を先に取ることがある。  
その瞬間、互いが相手のロックを待ち続けてデッドロック。  
