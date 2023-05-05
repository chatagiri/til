---
title: "AnsibleでWSL上のDocker containerをプロビジョニングする際に'muxclient: master hello exchange failed Failed to connect to new control master'"
date: 2023-05-05T00:00:00+09:00
categories:
  - ansible
tags:
  - ansible
  - docker
  - wsl
bookComments: false
bookSearchExclude: false
---
# AnsibleでWSL上のDocker containerをプロビジョニングする際に`muxclient: master hello exchange failed Failed to connect to new control master`のエラーが出る

## エラー発生まで
- WSL(Fedora)において、systemd上で動作するdocker + containerに対してansibleを実行しようとすると表題のエラー

```console
$ ansible -i hosts docker -m file -a "path=/var/tmp/test state=touch" -u root -k
SSH password: 
172.17.0.2 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: muxclient: master hello exchange failed\r\nFailed to connect to new control master",
    "unreachable": true
}
```

## 暫定対応
- ansible実行時に、`-e 'ansible_ssh_args="-o ControlMaster=no"`を指定する
```console
$ ansible -i hosts docker -m file -a "path=/var/tmp/test state=touch" -u root -k -e 'ansible_ssh_args="-o ControlMaster=no"'
```