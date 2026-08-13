設問68

次のコードのうち、正しく記述されているものを選べ（１つ）


A. Comparator<Integer> a = new Comparator<>(){

    public int compare(Integer a, Integer b){
     return a.compareTo(b);
    }

   };
   

B. Comparator b = new Comparator<>(){

    public int compare(Integer a, Integer b){
     return a.compareTo(b);
    }

   };
   

   
C. var c = new Comparator<>(){

    public int compare(Integer a, Integer b){
     return a.compareTo(b);
    }

   };
   
   
   
D. Comparator<> d = new Comparator<Integer>(){

    public int compare(Integer a, Integer b){
     return a.compareTo(b);
    }

   };
   
   
   
--------------------------------------

#選択肢判定


A:

```
Comparator<Integer> a = new Comparator<>(){
    public int compare(Integer a, Integer b){
        return a.compareTo(b);
    }
};

```

・左辺：Comparator<Integer> → OK  
・右辺：new Comparator<>() → ダイヤモンド演算子 OK  

**new Comparator<>() の <> は「ダイヤモンド演算子（diamond operator）」であり、“右辺の匿名クラスの型パラメータを 左辺の型から推論する” ための記法**


メソッド：compare(Integer, Integer) → 正しいオーバーライド  




B:

```
Comparator b = new Comparator<>(){
    public int compare(Integer a, Integer b){
        return a.compareTo(b);
    }
};
```

・左辺が raw type（Comparator） → 型安全でない  

・Java SE17 の試験では raw type は不正扱い  

→ ダイヤモンド演算子は 左辺の型情報を使って推論する  
→ しかし左辺が raw type のため 型推論ができない → コンパイルエラー  



C:

```
var c = new Comparator<>(){
    public int compare(Integer a, Integer b){
        return a.compareTo(b);
    }
};
```
var は 右辺の型から推論する必要がある  

右辺：new Comparator<>()   
→ ダイヤモンド演算子は 左辺の型情報が必要   
→ しかし左辺は var なので型情報がない  
→ 推論不能 → コンパイルエラー  

✘ コンパイルエラー（Java の型推論ルールに反する）  




D.

```
Comparator<> d = new Comparator<Integer>(){
    public int compare(Integer a, Integer b){
        return a.compareTo(b);
    }
};
```

左辺：Comparator<>    
→ ジェネリクスの <> は左辺では使えない  
→ 右辺の型推論に使うための構文であり、左辺では禁止  
**（ジェネリクスの型パラメータは 左辺では必ず具体的な型を書く必要がある）**

✘ 文法エラー（構文として不正）  