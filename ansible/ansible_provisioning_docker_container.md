---
title: "AnsibleでDocker containerをプロビジョニングする"
date: 2023-05-04T00:00:00+09:00
categories:
  - ansible
tags:
  - ansible
  - docker
  - wsl
bookComments: false
bookSearchExclude: false
---

# AnsibleでDocker containerをプロビジョニング
## テスト環境
- pythonとSSH入りの被provision Dockerコンテナ(AnsibleがSSHで接続し、python経由で命令解釈させる為必要)
  - https://hub.docker.com/r/eugenes1/python-sshd を使ってテストする
- docker containerを動かせる環境
```console
$ docker -v
Docker version 20.10.23, build %{shortcommit_cli}
```

- ansibleが叩ける環境
```
$ ansible --version
ansible [core 2.14.4]
...
python version = 3.11.2 (main, Feb  8 2023, 00:00:00) [GCC 12.2.1 20221121 (Red Hat 12.2.1-4)] (/usr/bin/python3)
```

## 動かしてみる
- 被provision docker container run && IP取得
```console
$ docker run -d  -p 2222:22  eugenes1/python-sshd
c75c3b9bddb9b1fdbe846fc48f528866c1c071c6a7936c72dab05a5efbb665f8

$ docker inspect c75c3b9bddb9b1fdbe846fc48f528866c1c071c6a7936c72dab05a5efbb665f8 | grep IPAddress
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.2",
                    "IPAddress": "172.17.0.2",

```

- ansible inventoryファイル作成
```console
$ vim hosts.yml
docker:
  hosts:
    172.17.0.2:
```

- コンソールからansible通ること確認
```console
$ ansible -i hosts docker -m file -a "path=/var/tmp/test state=touch" -u root -k -e ansible_python_interpreter=/usr/local/bin/python -e 'ansible_ssh_args="-o ControlMaster=no"'
SSH password: 
172.17.0.2 | CHANGED => {
    "changed": true,
    "dest": "/var/tmp/test",
    "gid": 0,
    "group": "root",
    "mode": "0644",
    "owner": "root",
    "size": 0,
    "state": "file",
    "uid": 0
}

$ docker exec c0691ca22d83 ls -l /var/tmp/test
-rw-r--r--    1 root     root             0 May  4 06:39 /var/tmp/test
```
