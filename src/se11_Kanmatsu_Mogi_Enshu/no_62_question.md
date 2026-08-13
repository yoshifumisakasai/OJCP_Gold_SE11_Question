設問62

次の3つのモジュール定義ファイルに関する説明として、正しいものを選べ（2つ）


□コード1

```
module api {

 exports com.sample.api;
}

```



□コード2

```
module provider {

 requires api;
 provides com.sample.api with com.test.impl;
}

```




□コード3

```
module client {
 requires api;
 uses com.sample.api;
}

```



A. providerモジュールは、実行時にcom.sample.apiのAPIを提供できる唯一のモジュールである


B. clientモジュールでproviderモジュールを要求する必要がある


C. providerモジュールでcom.test.implパッケージをエクスポートする必要がある


D. apiという独立したモジュールに配置すると、com.sample.apiのAPIを使用する複数のモジュールのインストールが容易になる