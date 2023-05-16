---
title: "Windows10 + WSL2(fedora)でsystemd管理の最新版dockerをインストールする"
date: 2023-05-02T00:00:00+09:00
categories:
  - wsl
tags:
  - wsl
  - docker
bookComments: false
bookSearchExclude: false
---

# Windows10 + WSL2(fedora)でsystemd管理の最新版dockerをインストールする
## 古いバージョンのdockerをアンインストールする
```console
# sudo dnf remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```

## リポジトリ setup
```console
# sudo dnf -y install dnf-plugins-core
# sudo dnf config-manager --add-repo  https://download.docker.com/linux/fedora/docker-ce.repo
```

## docker engine install
```console
# sudo dnf install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

## enable && start
```console
# sudo systemctl start docker
# sudo systemctl enable docker
```