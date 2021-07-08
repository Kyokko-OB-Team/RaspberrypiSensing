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
$ wget https://github.com/gari30/RasberryPi_Source/releases/download/<release名>/Temp_Humidi
```

### 実行方法

1. 温湿度センサとCO2センサを[こちら](https://docs.google.com/spreadsheets/d/1O9RdbZVYhcz8fl8laEi-iNipAEgiIhet7oFAs-LHp1w/edit)の資料を参考に接続してください。  
   ※上記リンクはGoogle Driveのスプレッドシートのリンクとなります。  
     PCブラウザ以外で開いた場合、貼り付けてある画像ファイルが見えない可能性がありますのでPCで開くようにしてください。

2. CO2センサはUART通信のため、[こちら](https://github.com/Kyokko-OB-Team/Document/wiki/raspberrypi_zero_enable_uart)を参考に、Raspberry Pi Zero WのUARTを有効化してください。

3. Temp_Humidiと同じディレクトリに、FireStoreの鍵ファイル(kyokko-ob-team_firestore.json)を配置し、実行してください。

```
$ ./Temp_Humidi
```

### CO2センサのキャリブレーションについて

CO2センサにはキャリブレーション機能があります。

正確な測定には必要になりますので、換気の良い状態に20分設置した後、キャリブレーションを実行してください。

キャリブレーションは以下のように、引数に「co2_init」をつけることで実行できます。

```
$ ./Temp_Humidi co2_init
co2 sensor calibration.
```

### バージョンについて

現在、バージョンによってCO2センサの有効/無効を分けております。

version.2.x : CO2センサ無し

version.3.x : CO2センサあり
