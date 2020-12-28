# jetson-nano


## 電源設定
デフォルトは5V 2A 電源を使う想定となっている。
5V 4A 電源を使用する場合は、J48にジャンパーピンを接続する必要がある。



## nvpmodel モード設定

設定値を確認
```bash
$ sudo nvpmodel -q
NVPM WARN: fan mode is not set!
NV Power Mode: MAXN
0
```

MAXモードに設定
```bash
$ sudo nvpmodel -m 0
$ sudo nvpmodel -q
NVPM WARN: fan mode is not set!
NV Power Mode: MAXN
0
```

デフォルトでMAXモードに設定されているみたい。

## jetson_clocks クロック設定

デフォルト値確認
```bash
$ sudo jetson_clocks --show
SOC family:tegra210  Machine:NVIDIA Jetson Nano Developer Kit
Online CPUs: 0-3
CPU Cluster Switching: Disabled
cpu0: Online=1 Governor=schedutil MinFreq=102000 MaxFreq=1479000 CurrentFreq=1326000 IdleStates: WFI=1 c7=1 
cpu1: Online=1 Governor=schedutil MinFreq=102000 MaxFreq=1479000 CurrentFreq=1479000 IdleStates: WFI=1 c7=1 
cpu2: Online=1 Governor=schedutil MinFreq=102000 MaxFreq=1479000 CurrentFreq=1036800 IdleStates: WFI=1 c7=1 
cpu3: Online=1 Governor=schedutil MinFreq=102000 MaxFreq=1479000 CurrentFreq=1132800 IdleStates: WFI=1 c7=1 
GPU MinFreq=76800000 MaxFreq=921600000 CurrentFreq=76800000
EMC MinFreq=204000000 MaxFreq=1600000000 CurrentFreq=1600000000 FreqOverride=0
Fan: speed=0
NV Power Mode: MAXN
```

MAXモードに設定
```bash
$ sudo jetson_clocks 
$ sudo jetson_clocks --show
SOC family:tegra210  Machine:NVIDIA Jetson Nano Developer Kit
Online CPUs: 0-3
CPU Cluster Switching: Disabled
cpu0: Online=1 Governor=schedutil MinFreq=1479000 MaxFreq=1479000 CurrentFreq=1479000 IdleStates: WFI=0 c7=0 
cpu1: Online=1 Governor=schedutil MinFreq=1479000 MaxFreq=1479000 CurrentFreq=1479000 IdleStates: WFI=0 c7=0 
cpu2: Online=1 Governor=schedutil MinFreq=1479000 MaxFreq=1479000 CurrentFreq=1479000 IdleStates: WFI=0 c7=0 
cpu3: Online=1 Governor=schedutil MinFreq=1479000 MaxFreq=1479000 CurrentFreq=1479000 IdleStates: WFI=0 c7=0 
GPU MinFreq=921600000 MaxFreq=921600000 CurrentFreq=921600000
EMC MinFreq=204000000 MaxFreq=1600000000 CurrentFreq=1600000000 FreqOverride=1
Fan: speed=0
NV Power Mode: MAXN
```

設定変更を設定ファイルに保存する。（${HOME}/l4t_dfs.confに保存される）
```bash
$ sudo jetson_clocks --store
```

設定ファイルの設定を読み込む。（${HOME}/l4t_dfs.confから読み込み）
```bash
$ sudo jetson_clocks --restore
```

再起動するとデフォルト値に戻る。
crontabを使用して、システム起動時に1度だけコマンドが実行する。
```bash
$ sudo vi /root/reboot.sh
#!/bin/sh

sleep 5
sudo nvpmodel -m 0
sleep 5
sudo jetson_clocks

$ sudo chmod 755 /root/reboot.sh
$ sudo crontab -e
@reboot /root/reboot.sh
```

## ファン設定

ファンを最大速度に設定
```bash
$ sudo sh -c 'echo 255 > /sys/devices/pwm-fan/target_pwm'
```

ファンを未使用に設定
```bash
$ sudo sh -c 'echo 0 > /sys/devices/pwm-fan/target_pwm'
```


