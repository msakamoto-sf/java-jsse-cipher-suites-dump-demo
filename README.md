# java-jsse-cipher-suites-dump-demo
dump jsse (Java Secure Socket Extension) default/supported TLS cipher suite name demo tool

JSSE(Java Secure Socket Extension) ��TLS���g���Ƃ��� Cipher Suite �ꗗ���_���v����f���ł��B
TLSv1, TLSv1.1, TLSv1.2 ���ꂼ��� SSLConetxt �����������AgetDefaultSSLParameters().getCipherSuites() �� getSupportedSSLParameters().getCipherSuites() �̌��ʂ�\�����܂��B

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


## ���s��

* 2019-01���_��Java8�œ���m�F���Ă��܂��B

## �J����

* AdoptOpenJDK 8 (jdk8u192-b12)
  * https://adoptopenjdk.net/
* Spring Tools 4 for Eclipse (Eclipse IDE 2018-12 R, 4.10�n)
  * https://spring.io/tools
* Maven >= 3.5.4 (maven-wrapper�ɂĎ����I��DL���Ă����)
* �\�[�X�R�[�h��e�L�X�g�t�@�C���S�ʂ̕����R�[�h��UTF-8���g�p

## �r���h�Ǝ��s

jar�t�@�C�����r���h���A`java -jar` �R�}���h�Ŏ��s���Ă��������B

```
cd java-jsse-cipher-suites-dump-demo/

�r���h:
./mvnw package

jar�t�@�C��������s:
java -jar target/java-jsse-cipher-suites-dump-demo-v201901.1.jar

crypto.policy=unlimited �w��(=JDK8�ŐV�̃f�t�H���g)�F
java -Djava.security.properties=java.security.crypto.policy-unlimited -jar target/java-jsse-cipher-suites-dump-demo-v201901.1.jar

crypto.policy=limited �w��F
java -Djava.security.properties=java.security.crypto.policy-limited -jar target/java-jsse-cipher-suites-dump-demo-v201901.1.jar
```

`java.security.properties` �v���p�e�B�ɂ�� `crypto.policy` �̃J�X�^�}�C�Y�ɂ��ẮA `(jdk_home)/jre/lib/security/java.security` �ݒ�t�@�C�����ɉ��������̂ł�������Q�Ƃ̂��ƁB

## Eclipse�v���W�F�N�g�p�̐ݒ�

https://github.com/SecureSkyTechnology/howto-eclipse-setup �� `setup-type2` ���g�p�BREADME.md�ňȉ����Q�Ƃ̂���:

* Clean Up/Formatter �ݒ�
* Git��clone����Maven�v���W�F�N�g�̃C���|�[�g

## �Q�l����

- https://docs.oracle.com/javase/jp/8/docs/technotes/guides/security/index.html
- Java Secure Socket Extension (JSSE)���t�@�����X�E�K�C�h
  - https://docs.oracle.com/javase/jp/8/docs/technotes/guides/security/jsse/JSSERefGuide.html
- Java�Í����A�[�L�e�N�`�� �W���A���S���Y�����̃h�L�������g(JDK 8�p)
  - https://docs.oracle.com/javase/jp/8/docs/technotes/guides/security/StandardNames.html
  - �� �uJSSE�Í��������Q���v�Q��

