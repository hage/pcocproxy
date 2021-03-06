pCocProxy as Persistent CocProxy
================================
めんどくさことしない置換プロキシーのキャッシュを永続化した変造版

詳しいことは[オリジナルのCocProxyを参照](http://coderepos.org/share/wiki/CocProxy)のこと。


使い方
------
起動時にオプション `--presistent` をつけるとキャッシュを永続化します。

キャッシュを消すときはオリジナルと同様URLに `?clearcache=1` をつけるか、
キャッシュディレクトリを以下のように消せばOKです。

    $ rm -rf /tmp/pcocproxy-cache


オリジナルとの相違点
--------------------
オリジナルはキャッシュとしてHashを利用していて、オンメモリで処理しており、
かつプロセスを終了させるとキャッシュは消えてしまいました。

この実装は速度がめちゃくちゃ速い利点がありました。
しかしせっかくためたキャッシュが綺麗さっぱりなくなってしまうとか、
メモリが厳しい環境で大量のキャッシュを保持すると泣きたくなるとか、
いろいろありました。というか私が泣きそうになりました。

なので多少速度は落ちますが、キャッシュをファイルに保持するようにして、
メモリをあんまり使わないこととキャッシュの永続化をはかりました。

「使い方」で書いたとおり、永続化オプションは `--persistent` です。
この場合はデフォルトのキャッシュディレクトリ `/tmp/pcocproxy-cache` を使います。
`--persistent=/path/to/cache/dir` のようにディレクトリを指定することもできます。


TODO
----
やるかどうかはしらんけどやるべきこと;
*  `proxy-config.yaml`で設定できるようにすべき
* キャッシュのデフォルトディレクトリを `files` の中にすべきか?
* ファイルの読み書き時にMutexで一律排他処理をかけてるが
  性能に悪影響ですよね。なんとかしたいです
