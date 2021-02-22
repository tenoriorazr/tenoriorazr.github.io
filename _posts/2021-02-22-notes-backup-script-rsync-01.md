---
layout: post
title:  "Backup com rsync 01"
date:   2021-02-22 09:35:00 -0300
categories: [scripts, linux, bash, rsync, backup]
---


&nbsp;


```sh
#!/bin/bash
# autor: evttenorio

DIR=/home/usuario/meusarquivos # DIRETÓRIO DE ORIGEM
DIRB=/home/usuario/backupmeusarquivos # DIRETÓRIO DE BACKUP
LIXEIRA=/home/usuario/recoverbackupfiles
DATA=`date +%B/%d-%m-%Y---%T`

echo $'\e[1;36m\U1F504 RSYNC [verbose-mode]\e[0m'
rsync --delete --backup-dir="$LIXEIRA/$DATA" -raAXtuv $DIR $DIRB
```

Ao ser executado, uma nova pasta é criada com o backup do diretório de origem. 

Sem preocupações com exclusão de arquivos enquanto o sript está em execução. 
Se algum arquivo da pasta de origem for deletado, tal arquivo irá para uma pasta que funciona como lixeira(recoverbackupfiles). 

Em *recoverbackupfiles* os arquivos deletados da pasta de origem estão organizados por mês. 
Alterando a formatação da variável `DATA` é possível ter uma organização diferente de quando os arquivos foram deletados.



#### Add no cronjobs

```bash
$ crontab -e
```

**Editando**

```bash
# Select shell mode
SHELL=/bin/bash


# sync the folders for every hours, for more: https://crontab.guru/every-1-hour
0 * * * * /home/usuario/backup-rsync-01.sh > /usuario/backup-rsync-01.log 2>&1
```