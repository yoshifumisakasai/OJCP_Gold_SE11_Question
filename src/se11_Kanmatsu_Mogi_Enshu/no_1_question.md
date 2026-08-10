設問1


このプログラムを次のコマンドで実行したときの結果として、正しく記述されているものを選べ（１つ）

```
package se11_Kanmatsu_Mogi_Enshu;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Sample {
	public static void main(String[] args) {
		try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
			System.out.print(" in: ");
			String input = br.readLine();
			System.out.println(" out: " + input);
		} catch (IOException e) {
			throw new RuntimeException(e);
		}
	}
}

```

java Sample hello


A. プログラム実行中に入力待ちになる

B. in: hello
   out: hello
   
C. in:
   out:
   
   
D. in:
   out:hello

E. 実行時に例外がスローされる


#ポイント
コードは 標準入力（stdin）からの入力 を BufferedReader で読み取っています。  
`String input = br.readLine();`  

「java Sample hello」の場合、hello は コマンドライン引数（args[0]） であり、標準入力には何も流れません。  
