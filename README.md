## PHP環境構築
ApacheがPHPプログラムを実行できように環境設定を行います。
```
	yum -y install php
	yum -y install php-devel
	yum -y install php-pdo
	yum -y install php-mysql
	yum -y install php-mbstring
```
本来であれば、拡張子が.phpのファイルをphp5-scriptハンドラで実行するようにApacheに指示する必要がありますが、yumからインストールした場合、インストールと同時に設定されるため、設定は不要です。
以下のページを開いて確認だけしておきましょう。
```
	vi /etc/httpd/conf.d/php.conf
```
## PHPの設定
まずオリジナルファイルをバックアップします。
```
	cp /etc/php.ini /etc/php.ini.org
```
PHPに関する設定は以下で変更できます。
```
	vi /etc/php.ini
```
ここでは以下の項目を変更しておきましょう。
- エラーの出力レベルを設定
```
	error_reporting = E_ALL & ~E_DEPRECATED&~E_NOTICE
```
- HTTPレスポンスヘッダで通知する文字エンコーディングを指定
```
	default_charset = "UTF-8"
```
- タイムゾーンの設定
```
	date.timezone = Asia/Tokyo
```
- PHP内でマルチバイト文字を扱う際の設定
- mb_send_mail関数を利用する時に使用するパラメータ
```
	mbstring.language = Japanese
```
- mbstring関数のデフォルトエンコード
```
	mbstring.internal_encoding = UTF-8
```
- 自動変換によるトラブル防止のため、自動変換させない設定
```
	mbstring.http_input = pass
	mbstring.http_output = pass
	mbstring.encoding_translation = Off
```
- 文字コード検出順序
```
	mbstring.detect_order = UTF-8,SJIS,EUC-JP,JIS,ASCII
```
- 文字コード変換に失敗した時の代替え文字。何もしないのnone
```
	mbstring.substitute_character = none;
```
設定ファイルの変更を有効にするにはApacheを再起動させる必要があります。
```
	/etc/init.d/httpd restart
```

