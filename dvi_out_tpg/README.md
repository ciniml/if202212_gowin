# DVI出力サンプル

## 概要

Tang Nano 9Kに搭載されているHDMIコネクタからDVI信号を出力するデザイン

## 合成の準備

いくつかのGOWIN EDA付属のIPを使用している。現状GOWINのIPはスクリプトからIPのHDLファイルを再生成することができないので、IP定義ファイルからの再生成をGUIを操作して手動で行う必要がある。

`src/tangnano9k/ip` 以下にある3つのIPを復元する。

* gowin_rpll
* gowin_rpll_ser

IPの復元はGOWIN EDAのGUI上の `Tools -> IP Core Generator` メニューから IP Core Generatorを開き、画面上部のボタンを押して各IPのディレクトリ下にある *.ipc ファイルを選択する。
その後、値を変更せずにOKを押すと、対象のIPのHDLファイルが生成される。

![IPCファイルの読み込み](./regenerate_ip.drawio.svg)

