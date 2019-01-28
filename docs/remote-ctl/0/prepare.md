# 事前準備 ～ SORACOM Air でインターネットに接続する

本章では、受講に先立って必要な環境構築の作業について説明します。

## <a id="software">ソフトウェアの準備</a>

ハンズオンで必要なソフトウェアをインストールします。

### Windows の場合

* TeraTerm 等 SSH が可能なソフトウェア

### macOS の場合

追加で準備する必要はありません。次へ進んでください。

## <a id="1-0">ユーザーコンソールを使用してAir SIMを管理する</a>

ここでは、SORACOM ユーザーコンソール(以降、ユーザーコンソール)を使用して、SORACOM AirのSIM (以降、Air SIM)をSORACOMのユーザーアカウントに登録します。ユーザーコンソールを使用するために、ユーザーアカウントの作成、および、支払情報の設定(クレジットカード情報)の登録を行います。

### <a id="1-1">SORACOM ユーザーアカウントの作成と設定</a>

ユーザーコンソールを使用するためには、SORACOMユーザーアカウント(以降、SORACOMアカウント)の作成が必要となります。アカウントの作成には、メールアドレスが必要となります。

### <a id="1-2">SORACOM アカウントの作成</a>

ユーザーコンソールをご利用いただくためには、まずSORACOM アカウントを作成してください。

https://console.soracom.io/#/signup にアクセスします。  
使用する SIM の種類を選択します。日本向けの SORACOM Air SIM を利用する場合は、カバレッジタイプ Japan を選択します。

![カバレッジ選択](images/reg0.png)

「アカウント作成」画面が表示されますのでメールアドレスおよびパスワードを入力します。また、契約者が個人であるか法人であるかを選び、法人の場合はさらに契約者の情報を入力します。最後に規約に同意するためのチェックボックスを入れ、「アカウントを作成」ボタンを押します。

[アカウントを作成] ボタンをクリックします。

![アカウント作成](images/reg1.png)

複数人でAir SIMの管理を行う場合は、事前にメーリングリストのアドレスを取得するなど、共有のメールアドレスをご利用ください。  
下記の画面が表示されるので、メールを確認してください。

![](images/reg2.png)

メールが届いたらリンクをクリックしてください。

![](images/reg3.png)

自動的にログイン画面に遷移しますので、メールアドレスとパスワードを入力してログインしてください。

### <a id="1-3">ユーザーコンソールへのログイン</a>

ログイン画面が表示されるので、アカウント作成時に登録したメールアドレスとパスワードを入力し、 [ログイン] ボタンをクリックしてください。(ログイン画面が表示されない場合はブラウザで https://console.soracom.io にアクセスします。)
![](images/reg4.png)

以下のような「SIM管理」画面が表示されたらログイン完了です。引き続き、支払情報の設定に進みましょう！
![](images/reg5.png)

### <a id="1-4">支払情報の設定</a>

通信料の支払い方法はクレジットカードになります。クレジットカードの情報を登録するには、メイン画面上部のユーザー名から[お支払い方法設定]を開きます。

![](images/reg6.png)

お支払方法で各情報を入力し、支払い方法を登録します。

![](images/reg7.png)

### <a id="1-5">ユーザーコンソールでの Air SIM の登録</a>

ユーザーコンソールにログインして、Air SIM の登録を行います。左上の [SIM登録] ボタンをクリックします。
![](images/reg8.png)


「SIM登録」画面で、Air SIM の台紙の裏面に貼ってある IMSI と PASSCODE を入力してください。

![](images/reg9.png)

名前、グループは空欄のままでも構いません。
「技術基準適合証明等について確認しました」チェックボックスを付けてください。
[登録] を押して SIM 登録を完了してください。（複数の Air SIM を続けて登録することも可能です。）

![](images/reg10.png)

Air SIM を登録した直後の状態は「準備完了」と表示され、通信可能な状態になっています。ただし、まだセッションは確立されていないので、セッション状態は「オフライン」になっていることを確認してください。

SORACOMではSIMの登録や「使用開始」「休止」「解約」といったモバイル通信の状態の更新をユーザー自身がユーザーコンソールを使用して、実施することが可能です。

なお、初めての通信、もしくは、ユーザーコンソール/APIで使用開始処理を行うことで、状態は「使用中」に変わります。 まだ通信を行いたくない場合は、ユーザーコンソールもしくはAPIで休止処理を行ってください。これにより「休止中」の状態となり通信は行われません。

## <a id="2-0">Raspberry Pi への接続</a>

SORACOMが実施するハンズオンでは、事前にOSを初期化した Raspberry Pi を用意してあります。  
割り当てられたRaspberryPiと、そのIPアドレスは運営が配布する資料をご確認ください。

### <a id="2-2">Windows をお使いの場合</a>

Windowsの場合には、TeraTerm等を使ってログインしてください。  
その際、ユーザ名は `pi` 、パスワードは `raspberry` を指定してください。

![teraterm](images/connect-air-01.png)

![teraterm](images/connect-air-02.png)

### <a id="2-1">macOS をお使いの場合</a>

自分の端末からRaspberry Piに接続(SSH)します。ターミナル(Terminal.app)を立ち上げ、以下のコマンドを実行してください。  

#### コマンド

```bash
ssh pi@192.168.123.xxx (割り当てられたIPアドレスを指定してください)
yes (初回接続時のみ)
raspberry
```

#### 参考: コマンドの実行結果

```text
~$ ssh pi@192.168.123.xxx (割り当てられたIPアドレスを指定してください)
The authenticity of host '192.168.123.xxx (192.168.123.xxx)' can't be established.
ECDSA key fingerprint is db:ed:1b:37:f2:98:c6:f4:d8:6d:cf:5c:31:6a:16:58.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.123.xxx' (ECDSA) to the list of known hosts.
pi@192.168.123.xxx's password: (raspberry と入力)

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Thu Sep 24 15:51:43 2015 from 192.168.123.yyy
pi@raspberrypi ~ $
```

## <a id="3-0">SORACOM Air SIMを使って、インターネットに接続する</a>

ここでは、先ほど登録したSORACOM AirのSIM (以降、Air SIM)を使用して、Raspberry Piからインターネットに接続します。

### <a id="3-1">Raspberry Pi に USBドングルを接続する</a>

![](images/3-1.jpg)

Air SIMを取り外します。Air SIMの端子を触らないように気をつけます。

![](images/3-2.jpg)
![](images/3-3.jpg)

<!--
TODO AK-020 版
![](images/3-4.jpg)
![](images/3-5.jpg)

#### Air SIMをドングルから取り出す際の注意

![](images/3-6.jpg)
-->

### <a id="3-2">接続スクリプトのダウンロード</a>

**ここから先の作業は、Raspberry Pi にログインしたターミナル(TeraTerm や Terminal.app 上)でコマンドを実行してください**

以下に、モデムの初期化、APNの設定、ダイアルアップなどを行うスクリプトが用意されています。

https://soracom-files.s3.amazonaws.com/setup_air.sh

以下のコマンドを実行し、このスクリプトをダウンロードし、接続用シェルスクリプトを作成します。

#### コマンド

```
curl -O https://soracom-files.s3.amazonaws.com/setup_air.sh
sudo bash setup_air.sh
```

#### 参考: コマンドの実行結果
```
pi@raspberrypi:~ $ curl -O https://soracom-files.s3.amazonaws.com/setup_air.sh

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  4040  100  4040    0     0  17211      0 --:--:-- --:--:-- --:--:-- 17264
pi@raspberrypi:~ $ sudo bash setup_air.sh
--- 1. Check required packages
wvdial is not installed! installing wvdial...
  :
  :
ok.

--- 2. Patching /lib/systemd/system/ifup@.service
ok.

--- 3. Generate config files
Adding network interface 'wwan0'.
Adding udev rules for modem detection.
ok.

--- 4. Connect
Found un-initilized modem. Trying to initialize it ...
Now you are all set.

Tips:
 - When you plug your usb-modem, it will automatically connect.
 - If you want to disconnect manually or connect again, you can use 'sudo ifdown wwan0' / 'sudo ifup wwan0' commands.
 - Or you can just execute 'sudo wvdial'.
```

これで、自動的に USB ドングル型モデムが初期化され、Raspberry Pi が SORACOM 経由でインターネットに接続します。 また、再起動時やモデムを接続した際にも、自動的に接続されるようになっています。

**このスクリプトをインストールするとRaspberry Pi が起動すると自動的にAir SIMでネットワーク接続が行われるようになります。データの送受信には通信料金が発生しますのでご注意ください。**

### <a id="3-3">接続確認する</a>

接続が出来ている時は、ppp0インターフェースが存在しているはずなので、以下のコマンドで接続状況を確認出来ます。

#### コマンド

```
ifconfig ppp0
```

#### 参考: コマンドの実行結果
```
pi@raspberrypi:~ $ ifconfig ppp0
ppp0      Link encap:Point-to-Point Protocol
          inet addr:10.xxx.xxx.xxx  P-t-P:10.64.64.64  Mask:255.255.255.255
          UP POINTOPOINT RUNNING NOARP MULTICAST  MTU:1500  Metric:1
          RX packets:133 errors:0 dropped:0 overruns:0 frame:0
          TX packets:134 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:3
          RX bytes:2092 (2.0 KiB)  TX bytes:4039 (3.9 KiB)
```

"inet addr" の後ろに表示されているのが、デバイスに割り当てられた IP アドレスとなります。

次に、インターネットへの疎通が出来るかどうかを確認しましょう。

Google Public DNS (8.8.8.8) への到達性を ping コマンドで調べます。

#### コマンド

※下記コマンドは、一行ずつ実行してください

```
ping 8.8.8.8
(Ctrl+C で止める)
```

#### 実行結果
```
pi@raspberrypi:~ $ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=55 time=343 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=55 time=342 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=55 time=361 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=55 time=340 ms
^C
--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3002ms
rtt min/avg/max/mdev = 340.908/347.329/361.814/8.434 ms
```

ping コマンドの応答からインターネットへの疎通が取れていることが確認できました。

## <a id="4-0">ユーザーコンソールによる通信の確認</a>

インターネットに接続できましたので、ユーザーコンソールからデータ通信量、利用料金を確認して、監視機能を設定しましょう。

### <a id="4-1">データ通信量と利用料金の確認</a>

#### Air SIMのデータ通信量の確認

ユーザーコンソールでは、データ通信量をSORACOM AirのSIM(以降、Air SIM)ごとにチャート形式で確認することができます。

データ通信量を確認したいAir SIMにチェックを入れ [詳細] ボタンをクリックします。

![](images/4-1.png)
[SIM 詳細] ダイアログが表示されますので、[通信量履歴] タブを開きます。 データ使用量は、表示期間を変更することもできます。

> データ通信量が反映されるまでに5〜10分かかります。先ほどのデータ通信が反映されていない場合はしばらくお待ちください。

![](images/4-2.png)

#### 利用料金の確認

ユーザーコンソールからデータ通信料金と基本料金を確認できます。
メイン画面左上部のボタンを押してメニューを出してから [課金情報] を選択します。

![](images/4-3.png)

表示されている時間時点の課金情報を確認することができます。

![](images/4-4.png)

また、画面下部にある [データ使用量実績データを CSV 形式でダウンロード] から、期間を選択して [ダウンロード] ボタンをクリックすることで、基本料金、転送データ量などの詳細を確認することができます。

```
 	請求額詳細のCSVには、IMSIごとに以下の項目が記載されています。
✓	date (日付)
✓	billItemName (basicCharge は基本料金、upload/downloadDataChargeは転送データ量に対する課金)
✓	quantity (数量: upload/downloadDataChargeの場合の単位はバイト)
✓	amount (金額: 日ごとの料金。この項目の総合計が、月額請求額となります)
✓	タグ、グループ
```

### <a id="4-2">監視機能の確認</a>

通信量にしきい値を設定し、超えた場合にメールでの通知と通信帯域制限をすることができます。監視できる項目は以下のとおりです。

-	各 SIM の日次通信量
-	各 SIM の今月の合計通信量
-	全ての SIM の今月の合計通信

例えば、全ての Air SIM の合計通信量が5000MB以上になった場合にメール通知を受けたい場合や、ある Air SIM の日次通信量が100MB以上になった場合にはその日の通信速度を制限するというような処理を行いたい場合に、この機能を利用することができます。

通信量はメガバイト単位（1以上の整数値）で入力できます。メールの宛先は登録されているメールアドレスです。通信速度を制限した場合は s1.minimum になり、解除された際は、 s1.standard に復帰します。 (APIを用いた場合には、制限時の通信速度、制限解除時の通信速度を任意に設定することも可能です)

Air SIMに監視の設定をしましょう。当ハンズオンの間に通知がくるように、1MiBで設定します。

「SIM詳細」画面で [監視] タブを開き、[SIM] をクリックして、監視設定を行ったら [設定を更新] ボタンをクリックして保存します。  

![](images/4-5.png)

ここでの設定は、対象のAir SIMごとに有効になります。

監視の設定は、以下の3つを対象することができます。
- Air SIM
- (Air SIMの所属する)グループ
- (登録した)全てのSIM

すぐに、メール通知を確認したい場合は、Raspberry Piから以下のコマンドを実行して、1MiBのダウンロードを実施してみてください。

#### コマンド

```
curl -o /dev/null http://soracom-files.s3.amazonaws.com/1MB
```

#### 参考: コマンドの実行結果

```
pi@raspberrypi:~ $ curl -o /dev/null http://soracom-files.s3.amazonaws.com/1MB
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 1024k  100 1024k    0     0   512k      0 --:--:-- --:--:-- --:--:--  512k
```

以下のような通知が届きます。(通知は最大で5分程度かかります。)

![](images/4-6.png)

## 以上で本章は終了です

達成状況を運営表へご記入ください。

* [目次ページへ戻る](../index)
