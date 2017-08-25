# Debian noroot 環境関連の差分ファイル集

## 概要

これは、 Debian noroot 環境における各種アプリケーションの動作の不具合等を修正するための差分ファイルです。

## 差分ファイルの内容

本節では、本差分ファイル集にある各差分ファイルの内容について述べます。

### dropbear-2017.75-fix.diff

軽量な SSH サーバである dropbear-2017.75 において、一部 bug fix を行い、 Debian noroot 環境において正常に動作させる為の差分ファイルです。

Android OS 5.0 における Debian noroot 環境において、擬似端末デバイスファイルである ```/dev/pts/*``` の所有権及び権限の変更が出来ない制約を回避し、また、システムコール ```link(2)``` の実行を回避しています。  
また、公開鍵暗号を用いた認証における不具合について bug fix を行っています。

なお、この差分ファイルを適用した dropbear-2017.75 のソースコードを Debian noroot 環境においてコンパイルするには、環境変数 ```CFLAGS``` に ```-DDEBIAN_NOROOT``` を設定する必要があります。