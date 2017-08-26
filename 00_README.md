# Debian noroot 環境関連の差分ファイル集

## 概要

これらの差分ファイルは、 [Debian noroot 環境][1]における各種アプリケーションの動作の不具合等を修正するための差分ファイルを集めた差分ファイル集です。

なお、これらの差分ファイルの作成に当たっては、 [termux の開発コミュニティ][2] による差分ファイルを参考にしました。

## 追記

### 2017/08/27 の追記

安定版の dropbear である [dropbear-2017.75][3] の差分ファイルに誤りがありましたので、訂正を行いました。

## 差分ファイルの内容

本節では、本差分ファイル集にある各差分ファイルの内容について述べます。

### dropbear-2017.75-fix.diff
### dropbear-HEAD-a5ec3aca.diff

軽量な SSH サーバである [dropbear-2017.75][3] 及び [github 上の dropbear][4] において、一部 bug fix を行い、 Debian noroot 環境において正常に動作させる為の差分ファイルです。

ここで、安定版の [dropbear-2017.75][3] には、差分ファイル ```dropbear-2017.75-fix.diff``` を、[github 上の dropbear][4] には、差分ファイル ```dropbear-HEAD-a5ec3aca.diff``` をそれぞれ適用して下さい。

これらの差分ファイルでは、 Android OS 5.0 における [Debian noroot 環境][1]において、擬似端末デバイスファイルである ```/dev/pts/*``` の所有権及び権限の変更が出来ない制約を回避し、また、システムコール ```link(2)``` の実行を回避しています。

また、公開鍵暗号を用いた認証における不具合について bug fix を行っています。

なお、この差分ファイルを適用した dropbear のソースコードを [Debian noroot 環境][1]においてコンパイルするには、環境変数 ```CFLAGS``` に ```-DDEBIAN_NOROOT``` を設定する必要があります。

[1]:https://play.google.com/store/apps/details?id=com.cuntubuntu&hl=ja
[2]:https://termux.com/
[3]:https://matt.ucc.asn.au/dropbear/releases/dropbear-2017.75.tar.bz2
[4]:https://github.com/mkj/dropbear