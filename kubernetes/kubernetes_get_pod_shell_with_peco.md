---
title: "pecoでk8s podのshellをよしなに取得する"
date: 2023-05-06T00:00:00+09:00
categories:
  - kubernetes
tags:
  - kubernetes
  - peco
bookComments: false
bookSearchExclude: false
---
# pecoでk8s podのshellをよしなに取得する
## pecoのインストール
- https://github.com/peco/peco/releases
```console
$ wget https://github.com/peco/peco/releases/download/v0.5.11/peco_linux_amd64.tar.gz
$ tar -zxvf peco_linux_amd64.tar.gz
$ sudo mv peco_linux_amd64/peco /usr/local/bin/peco
$ which peco
/usr/local/bin/peco
```

## shellを書く
```bash
#!/bin/bash

NAMESPACE=""
COMMAND="sh"

while getopts n:c: OPT
do
  case $OPT in
    n) 
      NAMESPACE=$OPT
    ;;
    c) 
      COMAMND=$OPT
    ;;
  esac
done

function peco-choosepod(){
  for podname in $(kubectl -n $NAMESPACE get pods | peco | awk '{print $1}' )
  do                                            
    echo "Login to $podname"
    kubectl exec -it $podname -- $COMMAND
  done
}

peco-choosepod $1
```

```console
$ chmod 755 ./getshell.sh
$ ./getshell.sh -n chatagiri -c /bin/bash
QUERY>                                                                                                                                                                                                                  IgnoreCase [67 (1/9)]
NAMESPACE        NAME                                                   READY   STATUS             RESTARTS   AGE                                                                                                                            
actpub-relay     actpub-relay-6bdcb7655-tdgzj                           3/3     Running            13         59d                                                                                                                            
blog             blog-wordpress-7769448449-qngm4                        0/1     Pending            0          86d                                                                                                                            
aiblog           wordpress-mysql-7c898fc494-vqfqn                       0/1     Pending            0          86d                                                                                                                            
cert-manager     cert-manager-5f6f7d784-zvpwq                           1/1     Running            2          35d                                                                                                                            
cert-manager     cert-manager-cainjector-845d589bfd-5shrh               1/1     Running            2          35d                                                                                                                            
cert-manager     cert-manager-webhook-777b87f99c-xwn2n                  1/1     Running            2          35d  
```