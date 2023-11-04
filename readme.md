# センサデータ取得アプリ

## これは何

Raspberry Pi Zero Wに接続した、温湿度センサとCO2濃度センサからのデータを  
ファイルとFireStoreに保存するアプリです。

## 使い方

### 動作環境

Raspberry Pi Zero Wでのみ、動作を確認しております。

### ダウンロード方法

[Releases](https://github.com/Kyokko-OB-Team/RasberryPi_Source/releases)にあるTemp_Humidiバイナリファイルをダウンロードして使用してください。

```
$ wget https://github.com/Kyokko-OB-Team/RasberryPi_Source/releases/download/<release名>/Temp_Humidi
```

### 必要なライブラリ

このプログラムでは以下のライブラリを使用しています。

- smbus
- serial
- firebase_admin

実行時にエラーが出る場合は、以下のようにライブラリをインストールしてください。
```
sudo apt install python3-smbus python3-pip
pip3 install pyserial
pip3 install grpcio==1.39.0
pip3 install firebase-admin==5.0.1
```

### 実行方法

1. 温湿度センサとCO2センサを[こちら](https://docs.google.com/spreadsheets/d/1O9RdbZVYhcz8fl8laEi-iNipAEgiIhet7oFAs-LHp1w/edit)の資料を参考に接続してください。  
   ※上記リンクはGoogle Driveのスプレッドシートのリンクとなります。  
     PCブラウザ以外で開いた場合、貼り付けてある画像ファイルが見えない可能性がありますのでPCで開くようにしてください。

1. 温湿度センサはI2C通信のため、[こちら](https://github.com/Kyokko-OB-Team/Document/wiki/raspberrypi_zero_enable_i2c)を参考に、Raspbery Pi ZeroのI2Cを有効化してください。

1. CO2センサはUART通信のため、[こちら](https://github.com/Kyokko-OB-Team/Document/wiki/raspberrypi_zero_enable_uart)を参考に、Raspberry Pi Zero WのUARTを有効化してください。

1. Temp_Humidiと同じディレクトリに、FireStoreの鍵ファイル(kyokko-ob-team_firestore.json)を配置します。
   鍵ファイルが存在しない場合は、firestoreへのpushを行いません。

1. 以下のように、第1引数に `--firestore` を指定し、第2引数にpush先のコレクション名を指定して実行してください。
   なお、指定しない場合は、firestoreへのpushを行いません。

```
$ ./Temp_Humidi --firestore [コレクション名]
```

### CO2センサのキャリブレーションについて

CO2センサにはキャリブレーション機能があります。

正確な測定には必要になりますので、換気の良い状態に20分設置した後、キャリブレーションを実行してください。

キャリブレーションは以下のように、引数に「co2_init」をつけることで実行できます。

```
$ ./Temp_Humidi co2_init
co2 sensor calibration.
```

### ビルド方法

以下のコマンドで、必要なモジュールをインストールしてください。
```
$ pip3 install pyinstaller
```
その後、リポジトリルートで`build.sh`を実行してください。
