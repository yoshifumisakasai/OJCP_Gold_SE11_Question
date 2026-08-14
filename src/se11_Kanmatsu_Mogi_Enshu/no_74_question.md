設問74

次のコードを確認してください。


```
public class Sample {

 public static void main(String[] args){
 
  new Sample().test(new int[] {4,3,2,1});
 }


 void test (int[] array) {
 
  int length = array.length;
  for(int i = 1; i < length; i++){
  
   int tmp = array[i];
   int n = i - 1;
   // code 1
   while( (-1 < n) && (array[i] < array[n])){
    // code 2
    array[n + 1] = array[n];
    n--;
    // dode 3
   }
   array[n + 1 ] = tmp;
   // code 4
  
  }
 
 }
}

```

配列arrayの要素がソートされたことを確認するには、code1～code4のどこに次のコードを挿入すればいいか（１つ選べ）

`assert n < 0 || array[n] <= array[n+1];`  


A. code 1

B. code 2

C. code 3

D. code 4
