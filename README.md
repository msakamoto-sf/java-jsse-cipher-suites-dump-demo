# java-jsse-cipher-suites-dump-demo
dump jsse (Java Secure Socket Extension) default/supported TLS cipher suite name demo tool

JSSE(Java Secure Socket Extension) でTLSを使うときの Cipher Suite 一覧をダンプするデモです。
TLSv1, TLSv1.1, TLSv1.2 それぞれで SSLConetxt を初期化し、getDefaultSSLParameters().getCipherSuites() と getSupportedSSLParameters().getCipherSuites() の結果を表示します。

```
    public static void main(String[] args) throws NoSuchAlgorithmException, KeyManagementException {
        final String[] protocols = new String[] { "TLSv1", "TLSv1.1", "TLSv1.2" };
        for (final String protocol : protocols) {
            final SSLContext sslContext = SSLContext.getInstance(protocol);
            sslContext.init(null, null, null);
            final List<String> defaultCipherSuites = Arrays
                    .asList(sslContext.getDefaultSSLParameters().getCipherSuites());
            Collections.sort(defaultCipherSuites);
            final List<String> supportedCipherSuites = Arrays
                    .asList(sslContext.getSupportedSSLParameters().getCipherSuites());
            Collections.sort(supportedCipherSuites);
            for (final String cn : defaultCipherSuites) {
                System.out.println(protocol + ",default," + cn);
            }
            for (final String cn : supportedCipherSuites) {
                System.out.println(protocol + ",supported," + cn);
            }
        }
    }
```


## 実行環境

* 2019-01時点でJava8で動作確認しています。

## 開発環境

* AdoptOpenJDK 8 (jdk8u192-b12)
  * https://adoptopenjdk.net/
* Spring Tools 4 for Eclipse (Eclipse IDE 2018-12 R, 4.10系)
  * https://spring.io/tools
* Maven >= 3.5.4 (maven-wrapperにて自動的にDLしてくれる)
* ソースコードやテキストファイル全般の文字コードはUTF-8を使用

## ビルドと実行

jarファイルをビルドし、`java -jar` コマンドで実行してください。

```
cd java-jsse-cipher-suites-dump-demo/

ビルド:
./mvnw package

jarファイルから実行:
java -jar target/java-jsse-cipher-suites-dump-demo-v201901.1.jar

crypto.policy=unlimited 指定(=JDK8最新のデフォルト)：
java -Djava.security.properties=java.security.crypto.policy-unlimited -jar target/java-jsse-cipher-suites-dump-demo-v201901.1.jar

crypto.policy=limited 指定：
java -Djava.security.properties=java.security.crypto.policy-limited -jar target/java-jsse-cipher-suites-dump-demo-v201901.1.jar
```

## Eclipseプロジェクト用の設定

https://github.com/SecureSkyTechnology/howto-eclipse-setup の `setup-type2` を使用。README.mdで以下を参照のこと:

* Clean Up/Formatter 設定
* GitでcloneしたMavenプロジェクトのインポート

