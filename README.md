# PHP環境構築
### ApacheがPHPプログラムを実行できように環境設定を行います。
```yum -y install php
   yum -y install php-devel
   yum -y install php-pdo
   yum -y install php-mysql
   yum -y install php-mbstring
```
本来であれば、拡張子が.phpのファイルをphp5-scriptハンドラで実行するようにApacheに指示する必要がありますが、yumからインストールした場合、インストールと同時に設定されるため、設定は不要です。
以下のページを開いて確認だけしておきましょう。
```vi /etc/httpd/conf.d/php.conf
```
