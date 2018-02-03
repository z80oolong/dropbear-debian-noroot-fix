# Debian noroot 環境において dropbear の動作に不具合が生じる問題を修正するための差分ファイル

## 概要

これらの差分ファイルは、 [Debian noroot 環境][DBNR]において、軽量な SSH サーバである [dropbear][DROP] のうち、安定版の [dropbear-2017.75][DR17] 及び [github 上の dropbear][DRRP] において、一部 bug fix を行い、 [Debian noroot 環境][DBNR]において正常に動作させる為の差分ファイルです。

これらの差分ファイルでは、 [Android OS 5.0][ANDR] における [Debian noroot 環境][DBNR]において、擬似端末デバイスファイルである ```/dev/pts/*``` の所有権及び権限の変更が出来ない制約を回避し、また、システムコール [```link(2)```][LINK] の実行を回避しています。

## 差分ファイルの適用とコンパイル

[dropbear][DROP] のソースコードに差分ファイルを適用するには、安定版の [dropbear-2017.75][DR17] には、差分ファイル ```dropbear-2017.75-fix.diff``` を、[github 上の dropbear][DRRP] には、差分ファイル ```dropbear-HEAD-8ffa8f72.diff``` をそれぞれ適用して下さい。

例えば、安定版の [dropbear-2017.75][DR17] のソースコードに ```dropbear-2017.75-fix.diff``` を適用するには、安定版の [dropbear-2017.75][DR17] のソースコードが置かれているディレクトリより、以下のようにして差分ファイル ```dropbear-2017.75-fix.diff``` を適用します。

```
 $ patch -p1 < /path/to/dropbear-2017.75-fix.diff
 (ここに、/path/to/diff は、 dropbear-2017.75-fix.diff が置かれたディレクトリのパス名)
```
そして、 [github 上の dropbear][DRRP] のソースコードに ```dropbear-HEAD-8ffa8f72.diff``` を適用するには、安定版の [github 上の dropbear][DRRP] のソースコードが置かれているディレクトリより、以下のようにして差分ファイル ```dropbear-HEAD-8ffa8f72.diff``` を適用します。

```
 $ patch -p1 < /path/to/dropbear-HEAD-8ffa8f72.diff
 (ここに、/path/to/diff は、 dropbear-HEAD-8ffa8f72.diff が置かれたディレクトリのパス名)
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

[github 上の dropbear][DRRP] の HEAD の commit である 8ffa8f72 に対応した差分ファイル ```dropbear-HEAD-8ffa8f72.diff``` を追加し、 obsolute となった差分ファイル ```dropbear-HEAD-a5ec3aca.diff```を削除しました。どうか御了承下さい。

<!-- 外部リンク一覧 -->

[DBNR]:https://play.google.com/store/apps/details?id=com.cuntubuntu&hl=ja
[ANDR]:https://www.android.com/intl/ja_jp/
[DROP]:https://matt.ucc.asn.au/dropbear/dropbear.html
[DR17]:https://matt.ucc.asn.au/dropbear/releases/dropbear-2017.75.tar.bz2
[LINK]:http://man7.org/linux/man-pages/man2/link.2.html
[DRRP]:https://github.com/mkj/dropbear
[TERM]:https://termux.com/