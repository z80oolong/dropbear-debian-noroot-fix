# Debian noroot 環境において dropbear の動作に不具合が生じる問題を修正するための差分ファイル

## 概要

これらの差分ファイルは、軽量な SSH サーバである [dropbear][DROP] のうち、安定版の [dropbear][DROP] 及び [github 上の dropbear][DRRP] において、一部 bug fix を行い、 [Debian noroot 環境][DBNR]において正常に動作させる為の差分ファイルです。

これらの差分ファイルでは、 [Android OS 5.0 以降][ANDR] における [Debian noroot 環境][DBNR]において、擬似端末デバイスファイルである ```/dev/pts/*``` の所有権及び権限の変更が出来ない制約を回避し、また、システムコール [```link(2)```][LINK] の実行を回避しています。

## 差分ファイルの適用とコンパイル

[dropbear][DROP] のソースコードに差分ファイルを適用するには、安定版の [dropbear][DROP] には、差分ファイル ```dropbear-x.y-fix.diff (ここに、 x.y は安定版のバージョン番号)``` を、[github 上の dropbear][DRRP] には、差分ファイル ```dropbear-HEAD-xxxxxxxx-fix.diff (ここに、 xxxxxxxx は、リビジョン番号)``` をそれぞれ適用して下さい。

例えば、安定版の [dropbear][DROP] のソースコードに ```dropbear-x.y-fix.diff``` を適用するには、安定版の [dropbear][DROP] のソースコードが置かれているディレクトリより、以下のようにして差分ファイル ```dropbear-x.y-fix.diff``` を適用します。

```
 $ patch -p1 < /path/to/dropbear-x.y-fix.diff
 (ここに、/path/to/diff は、 dropbear-x.y-fix.diff が置かれたディレクトリのパス名)
```
そして、 [github 上の dropbear][DRRP] のソースコードに ```dropbear-HEAD-xxxxxxxx.diff``` を適用するには、安定版の [github 上の dropbear][DRRP] のソースコードが置かれているディレクトリより、以下のようにして差分ファイル ```dropbear-HEAD-xxxxxxxx.diff``` を適用します。

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

## 追記

### 2017/08/27 の追記

安定版の [dropbear][DROP] である [dropbear-2017.75][DR17] の差分ファイルに誤りがありましたので、訂正を行いました。

### 2018/02/03 の追記

[github 上の dropbear][DRRP] の HEAD の commit である 8ffa8f72 に対応した差分ファイル ```dropbear-HEAD-8ffa8f72-fix.diff``` を追加し、 obsolute となった差分ファイル ```dropbear-HEAD-a5ec3aca-fix.diff```を削除しました。どうか御了承下さい。

### 2018/03/23 の追記

[github 上の dropbear][DRRP] の HEAD の commit である d740dc54 に対応した差分ファイル ```dropbear-HEAD-d740dc54-fix.diff``` を追加しました。これに伴い、差分ファイル ```dropbear-HEAD-8ffa8f72-fix.diff```を削除しました。どうか御了承下さい。

### 2017/04/13 の追記

安定版の [dropbear][DROP] である [dropbear-2018.76][DR18] に対応した差分ファイル ```dropbear-2018.76-fix.diff``` を追加しました。

### 2018/10/06 の追記

[github 上の dropbear][DRRP] の HEAD の commit である 6f6ef483 に対応した差分ファイル ```dropbear-HEAD-6f6ef483-fix.diff``` を追加しました。これに伴い、差分ファイル ```dropbear-HEAD-d740dc54-fix.diff```を削除しました。どうか御了承下さい。

<!-- 外部リンク一覧 -->

[DBNR]:https://play.google.com/store/apps/details?id=com.cuntubuntu&hl=ja
[ANDR]:https://www.android.com/intl/ja_jp/
[DROP]:https://matt.ucc.asn.au/dropbear/dropbear.html
[DR17]:https://matt.ucc.asn.au/dropbear/releases/dropbear-2017.75.tar.bz2
[DR18]:https://matt.ucc.asn.au/dropbear/releases/dropbear-2018.76.tar.bz2
[LINK]:http://man7.org/linux/man-pages/man2/link.2.html
[DRRP]:https://github.com/mkj/dropbear
[TERM]:https://termux.com/