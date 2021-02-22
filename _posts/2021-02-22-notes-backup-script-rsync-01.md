---
layout: post
title:  "Script de backup com rsync 01"
date:   2021-02-22 09:35:00 -0300
categories: [scripts, linux, bash, rsync, backup]
---


```sh
#!/bin/bash
# autor: evttenorio

DIR=/home/usuario/meusarquivos # DIRETÓRIO PRINCIPAL
DIRB=/home/usuario/backupmeusarquivos # DIRETÓRIO DE BACKUP
LIXEIRA=/home/usuario/recoverbackupfiles
DATA=`date +%B/%d-%m-%Y---%T`

echo $'\e[1;36m\U1F504 RSYNC [verbose-mode]\e[0m'
rsync --delete --backup-dir="$LIXEIRA/$DATA" -raAXtuv $DIR $DIRB
```

Ao ser executado, uma nova pasta é criada com o backup da "pasta principal". 

Se o script estiver full-time no crontab e algum arquivo da pasta principal seja deletado, 
tal arquivo irá para uma pasta que funciona como uma lixeira, 
desse modo não há preocupação com exclusão de arquivos enquanto o sript está em execução.
