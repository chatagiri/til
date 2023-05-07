---
title: "fail2banをインストールする"
date: 2023-05-07T00:00:00+09:00
categories:
  - fail2ban
tags:
  - fail2ban
  - linux
bookComments: false
bookSearchExclude: false
---
# fail2banをインストールする

## インストール && start
```console
# sudo dnf install fail2ban
# sudo systemctl enable fail2ban
# sudo systemctl start fail2ban
```

## 設定ファイル編集
```console
# sudo vim /etc/fail2ban/jail.conf


[sshd]
enabled = true
port = 22
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 120
```

## commands
```console
# fail2ban-client status 
Status
|- Number of jail:      0
`- Jail list:
```
