設問3

プログラマーが独自に作成する例外クラスに関する説明として、最も適切なものを選びなさい（１つ）


A. java.lang.RuntimeExceptionクラスのサブクラスでなければならない


B. java.lang.Exceptionクラスのサブクラスでなければならない


C. java.lang.Throwableクラスのサブクラスでなければならない


D. java.lang.Errorクラスのサブクラスでなければならない



独自に例外クラスを作る場合、Java の仕様では 必ず Throwable を継承する必要があります。
Exception や RuntimeException を継承するのが一般的ですが、
根本的なルールは 「Throwable のサブクラスであること」 です。
**Java の例外階層の最上位は Throwable。例外として扱われるには必ずこれを継承する**  
