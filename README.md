# radip.sh

[NHKラジオ](https://www.nhk.or.jp/radio/) / [radiko](http://radiko.jp/) / [ListenRadio](http://listenradio.jp/) / [渋谷のラジオ](https://shiburadi.com/) で現在配信中の番組を再生するシェルスクリプトです。

## フォーク元

うる。 ([@uru_2](https://twitter.com/uru_2)) さんの [radi.sh](https://github.com/uru2/radish)

## ライセンス

[MIT License](https://github.com/jeidii/radish/blob/master/LICENSE)

## 必要パッケージをインストール

````text
macOS:
brew install ffmpeg jq
````

````text
Linux:
sudo apt install -y curl ffmpeg jq libxml2-utils
````

## スクリプトをダウンロード

````text
macOS:
curl -LJO https://raw.githubusercontent.com/jeidii/radish/master/radip.sh
````

````text
Linux:
wget https://raw.githubusercontent.com/jeidii/radish/master/radip.sh
````

## 使い方

```text
sh radip.sh [options]
```

|引数|必須|説明|備考|
|:-|:-:|:-|:-|
|-t _SITE TYPE_|○|再生対象サイト|nhk: NHKラジオ<br>radiko: radiko<br>lisradi: ListenRadio<br>shiburadi: 渋谷のラジオ|
|-s _STATION ID_|△|放送局ID|`-l` オプションで表示されるID<br>渋谷のラジオは指定不要|
|-i _MAIL_| |ラジコプレミアム ログインメールアドレス|環境変数 `RADIKO_MAIL` でも指定可能|
|-p _PASSWORD_| |ラジコプレミアム ログインパスワード|環境変数 `RADIKO_PASSWORD` でも指定可能|
|-l| |放送局ID/名称表示|結果は300行以上になります、また取得は(割と)重いです|

## 実行例

````text
放送局ID/名称表示
sh radip.sh -l
````

```text
NHKラジオ
sh radip.sh -t nhk -s tokyo-fm
```

```text
radikoエリア内の局
sh radip.sh -t radiko -s LFR
```

```text
radikoエリア外の局 (ラジコプレミアム)
sh radip.sh -t radiko -s HBC -i "メールアドレス" -p "パスワード"
```

```text
radikoエリア外の局 (ラジコプレミアム, 環境変数からログイン情報設定)
export RADIKO_MAIL="メールアドレス"
export RADIKO_PASSWORD="パスワード"
sh radip.sh -t radiko -s HBC
```

```text
ListenRadio
sh radip.sh -t lisradi -s 30058
```

```text
渋谷のラジオ
sh radip.sh -t shiburadi
```

## プロセス操作

````text
ctrl+Z          # プロセスを一時停止
  jobs          # プロセスの管理状態を表示
    fg          # プロセスをフォアグランドで再開
    bg          # プロセスをバックグラウンドで再開

ctrl+C          # フォアグランドのプロセスを強制停止
killall ffplay  # プロセスを強制終了
````

## 注意点

再生手法については2019/5/25時点での調査結果であり、対象サイトの仕様変更等で利用できなくなる可能性もありますのであらかじめご了承ください。

## 動作確認環境

macOS 12.4

Linux

- Ubuntu 22.04
- WSL2 (Windows Subsystem for Linux 2)
