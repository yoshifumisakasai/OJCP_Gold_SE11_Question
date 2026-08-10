設問2

Unicode正規化を実現するためのメソッドとして、正しいものを選べ（１つ）


A. java.text.Normalizerクラスのnormalizeメソッド


B. java.text.Normalizerクラスのtranslateメソッド


C. java.text.Normalizationクラスのnormalizeメソッド


D. java.util.Normalizationクラスのtranslateメソッド


#ポイント(Java標準の正規化 API)  
Java で Unicode 正規化を行う公式 API は java.text.Normalizer であり、　　
正規化を実現するメソッドは normalize だけ。　　

`String normalized = Normalizer.normalize(input, Normalizer.Form.NFC);`  
