# インターフェース 2022年12月号 別冊付録1 サンプルコード

## 概要

本リポジトリは、インターフェース 2022年12月号 別冊付録1 2500円ボードで始めるFPGA開発 Vol.2 の応用編第3章、第4章で説明したデザインのソースコードを公開するためのものです。

## ディレクトリ構成

```
.
├── build_gowin.mk  // 共通ビルドスクリプト
├── cpu_matrix_led  // 第3章のソースコード
│   ├── Makefile
│   ├── project.tcl
│   └── src
│       ├── sw
│       │   ├── bootrom.c             // CPUのソフトウェアのソースコード
│       │   ├── bootrom.hex           // CPUのソフトウェアを$readmemhで読める形式に変換したもの 
│       │   ├── link.ld               // CPUのソフトウェア用のリンカ・スクリプト
│       │   └── Makefile              // CPUのソフトウェアをビルドするスクリプト
│       └── tangnano9k
│           ├── pins.cst
│           ├── timing.sdc
│           └── top.sv                // トップレベルモジュール
├── dvi_out_tpg     // 第4章のソースコード
│   ├── Makefile
│   ├── project.tcl
│   ├── README.md
│   ├── regenerate_ip.drawio.svg
│   └── src
│      ├── conv_logo.py    // ロゴの変換スクリプト
│      ├── interface_logo.bin  // ロゴの画像を2値画像に変換したバイナリデータ
│      ├── interface_logo.hex  // ↑を$readmemhで読めるように変換したもの
│      ├── sw
│      │   ├── bootrom.c   // CPUのソフトウェアのソースコード
│      │   ├── link.ld     // CPUのソフトウェア用のリンカ・スクリプト
│      │   └── Makefile    // CPUのソフトウェアをビルドするスクリプト
│      └── tangnano9k
│          ├── iobuf_sim.sv
│          ├── ip
│          │   ├── gowin_rpll
│          │   │   └── gowin_rpll.ipc  // ビデオ信号用rPLLの定義ファイル
│          │   └── gowin_rpll_ser
│          │       └── gowin_rpll_ser.ipc  // シリアライザ用rPLLの定義ファイル
│          ├── Makefile    // デザインのビルドスクリプト
│          ├── pins.cst    // ピン定義
│          ├── reset_seq.sv
│          ├── tb.sv
│          ├── timing.sdc
│          └── top.sv      // トップレベルモジュールのHDL
├── external
│   └── picorv32    // PicoRV32のリポジトリ
├── README.md       // 本ファイル
├── rtl
│   ├── dvi_out
│   │   └── dvi_out.sv  // DVI出力モジュール (TMDSエンコーダ)
│   └── video
│       └── test_pattern_generator.sv   // テストパターン生成モジュール
└── targets
    └── tangnano9k
        └── target.mk
```

## 使い方

### 共通

* GOWIN EDAをインストールしたのち、 `IDE/bin` ディレクトリにパスを通しておきます。
* openFPGALoaderをインストールしておきます。

### DVI映像出力

* `dvi_out_tpg/src/tangnano9k/ip` 以下の `gowin_rpll/gowin_rpll.ipc` `gowin_rpll_ser/gowin_rpll_ser.ipc` を、GOWIN EDAのGUIから開き、IPのHDLを再生成します。
    * 詳しくは [こちら](dvi_out_tpg/README.md) を参照してください。
 
* `dvi_out_tpg/src/tangnano9k` 以下で `make` を実行します。
* Tang Nano 9KをPCに接続し、 `make run` を実行すると、FPGAに合成したデザインを書き込んで実行します。 
* HDMIコネクタとPC用ディスプレイを接続すると、画面にInterface誌のロゴが跳ね回る映像が表示されます。

### CPU制御マトリクスLED

* 基礎編第4章のマトリクスLED回路を組み立てます。
* `cpu_matrix_led/src/tangnano9k` 以下で `make` を実行します。
* Tang Nano 9KをPCに接続し、 `make run` を実行すると、FPGAに合成したデザインを書き込んで実行します。 


## ライセンス

本リポジトリに自体に含まれているHDLはすべてBoost Software License 1.0の下で利用可能です。
非常に単純に説明すると、ソースコードに含まれているライセンス表記さえ残せば、派生物のバイナリ等に対してはとくにライセンス表記等が不要なライセンスです。
詳しくはリポジトリに含まれている [LICENSE](./LICENSE)  か、Boostのサイトを確認してください (https://www.boost.org/users/license.html)

但し、external以下にsubmoduleとして取り込んでいるPicoRV32や、GOWIN EDAで再生成したGOWIN IPのHDL等に関しては、それぞれのライセンスに従います。