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
---------------------------------------------------------------------------
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
---------------------------------------------------------------------------
## PHPプログラミング基礎
- コードブロック

PHPコードは「<?php」という開始タグから開始し、終了タグは「?>」です。
```
	<?php
		//phpコードを記述
	?>
```
- 文字列の出力

phpで文字列を出力した場合、printまたはechoを使います。　
お好みのほうを使用してください。
```
	example1.php
	
	<?php
		//文字列の出力
		print "<p>HelloWorld!</p>";
		echo "<p>HelloWorld!</p>";
	?>
```
- コメント

一行コメントを挿入したい場合は「//」を先頭に追加します。　
複数行コメントを挿入したい場合は「/*」ではじめ、コメントを記述し終わったら「*/」で閉じます。
```
	<?php
		// 一行コメント
		/*
		複数行コメント
		複数行コメント
		*/
	?>
```
- 変数

変数は代入された値を維持する記憶領域です。　
PHPは明示的な型を持たず、値が代入された時に自動的に型が決定します。　
PHPは先頭に```$```記号をつけることで変数として認識されます。
```
	example2.php
	
	<?php
		$a = 'string'; //変数$aを定義
		$i = 1; //変数$iを定義
		print $a;
		print '<br/>';
		print $i;
	?>
```
- 型の種類

	論理型(bool)：真と偽の２値をもつ型です。

	整数型(integer)：整数値を表現する型です。

	浮動小数点型(double)：実数値を表現する型です。

	文字列型(string)：文字列を表現する型です。

	配列型(array)：複数のデータを保持することが可能な型です。

	オブジェクト型(object)：複数のデータと関数をもった型です。

	ヌル型(null)：変数が値をもたないことを表現した型です。


