# Debian noroot 環境において dropbear の動作に不具合が生じる問題を修正するための差分ファイル

## 概要

これらの差分ファイルは、 [Debian noroot 環境][1]において、軽量な SSH サーバである [dropbear][2] のうち、安定版の [dropbear-2017.75][3] 及び [github 上の dropbear][4] において、一部 bug fix を行い、 Debian noroot 環境において正常に動作させる為の差分ファイルです。

これらの差分ファイルでは、 Android OS 5.0 における [Debian noroot 環境][1]において、擬似端末デバイスファイルである ```/dev/pts/*``` の所有権及び権限の変更が出来ない制約を回避し、また、システムコール ```link(2)``` の実行を回避しています。

また、 [github 上の dropbear][4] においては、公開鍵暗号を用いた認証における不具合について bug fix を行っています。

## 追記

### 2017/08/27 の追記

安定版の [dropbear][2] である [dropbear-2017.75][4] の差分ファイルに誤りがありましたので、訂正を行いました。

## 差分ファイルの適用とコンパイル

[dropbear][2] のソースコードに差分ファイルを適用するには、安定版の [dropbear-2017.75][3] には、差分ファイル ```dropbear-2017.75-fix.diff``` を、[github 上の dropbear][4] には、差分ファイル ```dropbear-HEAD-a5ec3aca.diff``` をそれぞれ適用して下さい。

なお、これらの差分ファイルを適用した [dropbear][2] のソースコードを [Debian noroot 環境][1]においてコンパイルするには、環境変数 ```CFLAGS``` に ```-DDEBIAN_NOROOT``` を設定する必要があります。

## 謝辞

なお、これらの差分ファイルの作成に当たっては、 [termux の開発コミュニティ][5] による差分ファイルを参考にしました。 [termux の開発コミュニティ][5]の皆様には心より感謝致します。

<!-- URL Reference -->

[1]:https://play.google.com/store/apps/details?id=com.cuntubuntu&hl=ja
[2]:https://matt.ucc.asn.au/dropbear/dropbear.html
[3]:https://matt.ucc.asn.au/dropbear/releases/dropbear-2017.75.tar.bz2
[4]:https://github.com/mkj/dropbear
[5]:https://termux.com/