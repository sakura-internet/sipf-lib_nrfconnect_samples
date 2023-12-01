# さくらのモノプラットフォーム Client library for nRFConnect サンプルプログラム集

[さくらのモノプラットフォーム Client library for nRFConnect](https://github.com/sakura-internet/sipf-lib_nrfconnect)の[v231030](https://github.com/sakura-internet/sipf-lib_nrfconnect/releases/tag/v231030)に対応したサンプルプログラム集です。

対応するnRF Connect SDKはv2.4.2です。

本サンプル集のビルドにはnRF Connect SDKが必要です。  
事前に[nRF Connect for Desktop](https://www.nordicsemi.com/Products/Development-tools/nRF-Connect-for-Desktop)等を使用して、対象となるバージョンのSDKがインストールされていることを前提としています。

## ディレクトリ構成

```
sipf-lib_nrfconnect_samples
|
+- lib (さくらのモノプラットフォーム Client library for nRFConnect(sipf-lib_nrfconnect) v231030のソースコード)
|
+- samples
   |
   +- file_download (ファイル受信)
   |
   +- file_upload (ファイル送信)
   |
   +- object_rx (オブジェクト受信)
   |
   +- object_tx (オブジェクト送信)
```

## サンプルプログラム

以下のサンプルプログラムが含まれます。

- オブジェクト送信 [object_tx](samples/object_tx/)
- オブジェクト受信 [object_rx](samples/object_rx/)
- ファイル送信 [file_upload](samples/file_upload/)
- ファイル受信 [file_download](samples/file_download/)

### サンプルプログラムのビルド方法

ビルドしたいサンプルプログラムのディレクトリに移動しnRF Connect SDKの`west`コマンドでビルドおよび書き込みを行います。  
ターゲットボードなどの詳細は各プログラムのREADMEを参照してください。

#### 例: SCM-LTEM1NRF向けにオブジェクト送信サンプルプログラムをビルドし、書き込む場合

```
$ cd samples/object_tx
$ west build -b scm-ltem1nrf_nrf9160_ns
  :
  :
  :
Memory region         Used Size  Region Size  %age Used
           FLASH:      114884 B       992 KB     11.31%
             RAM:       36832 B     211608 B     17.41%
        IDT_LIST:          0 GB         2 KB      0.00%
[287/287] Generating zephyr/merged.hex

$ west flash
```
