---
title: "Windows10 + WSL2(fedora)でsystemd管理のDocker環境を作る"
date: 2023-05-02T00:00:00+09:00
# bookComments: false
# bookSearchExclude: false
---

# Windows10 + WSL2(fedora)でsystemd管理のDocker環境を作る

## WSL2をインストールする
- powershellからwsl2 install
```console
@powershell
---
PS C:\> wsl --install
PS C:\> wsl --set-default-version 2
```

## 任意のLinux Distributionを入れて初回起動する
  - Microsoft Storeで、"wsl + [distribution名]" で検索して、使いたい奴を入れる。
    - fedoraなら "Fedora Remix"を入れると良さそう。
  - 一回起動してユーザ設定を済ませておく。

## wslをsystemd enableで起動する

- wsl.confにsystemd有効化設定を追加する
```
@wsl
---
# sudo vim /etc/wsl.conf

[boot]
systemd=true
```


- wsl 再起動する
```
@powershell
---
PS C:\> wsl --shutdown
```

## dockerをインストールして起動する
- docker インストール&&再起動時有効化
```
@wsl
---
# sudo dnf install docker
# sudo systemctl enable docker
# sudo systemctl start docker
# sudo systemctl status docker

● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: disabled)
     Active: active (running) since Tue 2023-05-02 19:29:58 JST; 29s ago
```

## 操作ユーザからdockerコマンドを叩けるようにする

- 操作ユーザをdocker groupに追加する
```
@wsl
---
# sudo usermod -aG docker $(whoami)
```

- wsl 再起動する
```
@powershell
 - 再起動しないとgroup設定が反映されないらしい
 - user exitでconsole握り直しじゃダメだった
---
PS C:\> wsl --shutdown
```

- 確認
```
@wsl
---
$ id $(whoami)
uid=1000(USERNAME) gid=1000(USERNAME) groups=1000(USERNAME),4(adm),10(wheel),11(cdrom),39(video),44(wsl-video),996(docker)
// docker groupが追加されていること

$ ls -l /var/run/docker.sock
srw-rw---- 1 root docker 0 May  2 20:26 /var/run/docker.sock
// docker.sockの所有者groupがdockerなこと

$ docker run hello-world
...
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
// めでたいメッセージが表示されていること
```

## docker-composeをインストールする
- docker-compose install
```
# sudo dnf update
# sudo dnf install docker-compose-plugin
```
