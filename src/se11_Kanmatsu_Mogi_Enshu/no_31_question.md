設問31

モジュールを定義している。次のモジュール定義ファイルに関する説明として、正しいものを選べ（１つ）


```
module Sample {

 exports test;
 uses test.Hello;

}

```


A. コンパイルエラーを発生させないためには、test.Helloを実装するモジュールが1つ以上モジュールパスに含まれている必要がある


B. エラーを発生せずに実行するには、test.Helloを実装するモジュールが、1つ以上モジュールパスに含まれている必要がある


C. test.Helloの実装をSampleモジュールに追加できる


D. test.Helloを実装するモジュールは、モジュール定義ファイルに「requires Sample;」というディレクティブを含める必要がある


E. test.Helloを実装するモジュールは、Sampleモジュールを再コンパイルせずにコンパイルおよび追加できる



#JPMS（Java Platform Module System）の “uses / provides” の仕組み  

・サービス提供側は 別モジュールで 「provides ... with ...」 を書く必要がある。  
D. 実装モジュールは requires Sample を含める必要はない  
   サービス提供側は Sample を参照する必要はない。
必要なのは：
`provides test.Hello with 実装クラス;`  


・uses は “サービスを利用する側” の宣言であり、  
サービス提供モジュール（provides を持つモジュール）は後から追加しても Sample モジュールの再コンパイルは不要。  

■🔍 モジュール定義の意味

```
module Sample {
    exports test;
    uses test.Hello;
}
```

◆ exports test;
→ test パッケージを外部に公開する。

◆ uses test.Hello;
→ **Sample モジュールは サービスインタフェース test.Hello を利用する側**    
→ **つまり サービスローダー（ServiceLoader）で test.Hello の実装を探す。**  

#ポイント：uses は「実装がなくてもコンパイルできる」

**uses は サービスの利用宣言であり、コンパイル時に 実装が存在する必要はない。**    

・実装がなくてもコンパイルできる  

・実行時に ServiceLoader が見つけられなければ null になるだけ  

・実装モジュールは後から追加可能  

・Sample モジュールを再コンパイルする必要はない  
(JPMS のサービスローダーは 動的にサービス提供モジュールを追加できる。)  
(Sample モジュールを再コンパイルせずに実装モジュールを追加できる)  

---------------------------------------------------------------------------------


#✅ モジュール構成（コード）  

◆ 1. Sample モジュール（サービス利用側）
■module-info.java

```
module Sample {
    exports test;
    uses test.Hello;   // ← Hello の「実装を使う側」
}
```

■test/Hello.java（サービスインタフェース）

```
package test;

public interface Hello {
    void hello();
}
```

■Sample モジュールのコード（ServiceLoader を使う）

```
package test;

import java.util.ServiceLoader;

public class Main {
    public static void main(String[] args) {
        ServiceLoader<Hello> loader = ServiceLoader.load(Hello.class);

        for (Hello h : loader) {
            h.hello();
        }
    }
}
```

◆ 2. Hello の実装モジュール（サービス提供側）
■module-info.java

```module HelloImpl {
    requires Sample;  // ← Sample の Hello インタフェースを使うために必要
    provides test.Hello with impl.HelloImpl;  // ← Hello の実装を提供
}
```

■impl/HelloImpl.java

```
package impl;

import test.Hello;

public class HelloImpl implements Hello {
    @Override
    public void hello() {
        System.out.println("Hello from Impl");
    }
}
```
