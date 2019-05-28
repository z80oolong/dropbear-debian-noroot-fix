# Debian noroot 環境において dropbear の動作に不具合が生じる問題を修正するための差分ファイル

## 概要

この差分ファイルは、軽量な SSH サーバである [dropbear][DROP] のうち、安定版の [dropbear][DROP] 及び [github 上の dropbear][DRRP] において、一部 bug fix を行い、 [Debian noroot 環境][DBNR]において正常に動作させる為の差分ファイルです。

これらの差分ファイルでは、 [Android OS 5.0 以降][ANDR] における [Debian noroot 環境][DBNR]において、擬似端末デバイスファイルである ```/dev/pts/*``` の所有権及び権限の変更が出来ない制約を回避し、また、システムコール [```link(2)```][LINK] の実行を回避しています。

## 差分ファイルの適用とコンパイル

[dropbear][DROP] のソースコードに差分ファイルを適用するには、安定版の [dropbear][DROP] には、差分ファイル ```dropbear-x.y-fix.diff (ここに、 x.y は安定版のバージョン番号)``` を、[github 上の dropbear][DRRP] には、差分ファイル ```dropbear-HEAD-xxxxxxxx-fix.diff (ここに、 xxxxxxxx は、リビジョン番号)``` をそれぞれ適用して下さい。

例えば、安定版の [dropbear][DROP] のソースコードに ```dropbear-x.y-fix.diff``` を適用するには、安定版の [dropbear][DROP] のソースコードが置かれているディレクトリより、以下のようにして差分ファイル ```dropbear-x.y-fix.diff``` を適用します。

```
 $ patch -p1 < /path/to/dropbear-x.y-fix.diff
 (ここに、/path/to/diff は、 dropbear-x.y-fix.diff が置かれたディレクトリのパス名)
```
そして、 [github 上の dropbear][DRRP] のソースコードに ```dropbear-HEAD-xxxxxxxx.diff``` を適用するには、 [github 上の dropbear][DRRP] のソースコードが置かれているディレクトリより、以下のようにして差分ファイル ```dropbear-HEAD-xxxxxxxx.diff``` を適用します。

```
 $ patch -p1 < /path/to/dropbear-HEAD-xxxxxxxx.diff
 (ここに、/path/to/diff は、 dropbear-HEAD-xxxxxxxx.diff が置かれたディレクトリのパス名)
```

なお、これらの差分ファイルを適用した [dropbear][DROP] のソースコードを [Debian noroot 環境][DBNR]においてコンパイルするには、```./configure``` コマンドの実行時に以下のようにして、環境変数 ```CFLAGS``` に ```-DDEBIAN_NOROOT``` を設定する必要があります。

```
 $ CFLAGS="-DDEBIAN_NOROOT" ./configure --prefix=...  # (以下、適宜オプションを設定すること。)
```

## 謝辞

なお、これらの差分ファイルの作成に当たっては、 [termux の開発コミュニティ][TERM] による差分ファイルを参考にしました。 [termux の開発コミュニティ][TERM]の皆様には心より感謝致します。

最後に、 [Matt Johnston 氏を始めとした dropbear の開発コミュニティの関係各位][DROP]及び [dropbear][DROP] に関わった方々の全てに心より感謝致します。

## 使用条件

本差分ファイルは軽量な SSH サーバである [dropbear][DROP] に適用する差分ファイルであり、 [Z.OOL. (mailto:zool@zool.jpn.org)][ZOOL] が著作権を有します。

従って、本差分ファイルは [dropbear][DROP] のライセンスと同様である [MIT License][MITL] に基づいて配布されるものとします。詳細については、本リポジトリに同梱する ```LICENSE``` を参照して下さい。

<!-- 外部リンク一覧 -->

[DBNR]:https://play.google.com/store/apps/details?id=com.cuntubuntu&hl=ja
[ANDR]:https://www.android.com/intl/ja_jp/
[DROP]:https://matt.ucc.asn.au/dropbear/dropbear.html
[LINK]:http://man7.org/linux/man-pages/man2/link.2.html
[DRRP]:https://github.com/mkj/dropbear
[TERM]:https://termux.com/
[ZOOL]:http://zool.jpn.org/
[MITL]:http://www.opensource.org/licenses/mit-license.php
