# オブジェクト受信サンプルプログラム

本ソフトウェアは[さくらのモノプラットフォーム](https://iot.sakura.ad.jp/platform/)の`オブジェクト受信`のサンプルプログラムです。

[さくらのモノプラットフォーム Client library for nRFConnect](https://github.com/sakura-internet/sipf-lib_nrfconnect)の[SIPF_OBJECT: オブジェクト送受信クライアント](https://github.com/sakura-internet/sipf-lib_nrfconnect/wiki/SIPF_OBJECT)を使用しています。

ターゲットデバイスは以下の通りです。

- [Nordic nRF9160DK](https://www.nordicsemi.com/Products/Development-hardware/nRF9160-DK)
- [Nordic Thingy:91](https://www.nordicsemi.com/Products/Development-hardware/Nordic-Thingy-91)
- [SakuraInternet SCM-LTEM1NRF](https://iot.sakura.ad.jp/platform/service/dev-kit/)

## プログラムについて

### 動作

電源をONにするとPOWER LEDが点灯します。

その後、LTE接続が完了しさくらのモノプラットフォームと通信可能になるとSTATUS LEDが点滅します。  
ターミナルには`+++ Ready +++`と表示されます。

STATUS LEDが点滅している状態で受信ボタンを押すたびに`さくらのモノプラットフォーム`に届いている自分宛てのオブジェクトを取得します。

以下の`Tag ID`と`Type`に一致するオブジェクトを受信した場合、LEDの点灯/消灯を切り替えます。

| Tag ID | Type | 内容 |
|-|-|-|
| 0x00 | UINT8 | LED1の点灯状態 (0:OFF, 0以外: ON)|
| 0x01 | UINT8 | LED2の点灯状態 (0:OFF, 0以外: ON)|

上記以外の組み合わせのオブジェクトを受信した場合、ターミナルに`Tag ID`と`Type`を表示します。(値は表示しません)

受信が完了するとターミナルに、オブジェクト転送ID(OTID)が表示されます。

### 使用するIO

ターミナル等からの入出力にUART、受信ボタンLED1、LED2としてGPIOを使用します。

#### UART

通信設定は以下のとおりです。

- BOUD 115200bps
- DATA 8bit
- STOP 1bit
- PARITY none
- FLOW none

改行コードはCR+LFです。

#### 受信ボタン

| ボード | 受信ボタン |
|-|-|
| nRF9160DK | `Button1` |
| Thingy:91 | `SW3` |
| SCM-LTEM1NRF | `PIN20` |

論理はACTIVE-LOです。

#### LED

| ボード | LED1 | LED2 |
|-|-|-|
| nRF9160DK | `LED3` | `LED4` |
| Thingy:91 | `RED LED` | `BLUE LED` |
| SCM-LTEM1NRF | `PIN6` | `PIN6` |

論理はACTIVE-HIです。

## ビルド

ビルドには `west build` コマンドを使用します。

```
west build -b [board]
```

`board` には以下のパラメータを指定することができます。

- nrf9160dk_nrf9160_ns
- thingy91_nrf9160_ns
- scm-ltem1nrf_nrf9160_ns

例: Nordic nRF9160DK 向けにビルドする場合
```
west build -b nrf9160dk_nrf9160_ns
```

## クリーン

ビルドの出力ディレクトリ `build` を削除します。

```
rm -rf build
```

## 書き込み

書き込みには `west flash` コマンドを使用する方法とビルド結果のHEXファイルをツールを使用する方法があります。

### west flash コマンドを使用する場合

```
west flash
```

`west flash` コマンドは内部で `nrfjprog` コマンドを実行するので事前に[nRF Command Line Tools](https://www.nordicsemi.com/Products/Development-tools/nRF-Command-Line-Tools)のインストールが必要です。

### ツールを使用する場合

ビルド結果のHEXファイル `build/zephyr/merged.hex` を [nRF Connect for Desktop](https://www.nordicsemi.com/Products/Development-tools/nRF-Connect-for-Desktop)に含まれる `Programmer` アプリケーションで書き込んでください。


---
本プログラムで使用している `さくらのモノプラットフォーム Client library for nRFConnect` については [Wiki](https://github.com/sakura-internet/sipf-lib_nrfconnect/wiki) を参照してください。
