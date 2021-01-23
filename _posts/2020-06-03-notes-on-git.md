---
layout: post
title:  "Notas sobre git"
date:   2020-06-03 08:30:00 -0300
categories: [git]
---

* O básico do git *
Comandos úteis do git para já começar usá-lo.

**Criar o repositório.** 
- Criar em New Repository/Project. 
- Adicionar nome e descrição.

**Configuraçao Inicial**
```
git config --global user.name "Myname"
git config --global user.mail "myemail@emails.com"
git config --global core.editor "editor(vim, vi, etc)"
```

_Exibindo configurações_
```
git config --list
git config user.name
```

**Fazer do diretório atual um projeto git e adicione ".git"**
 ```
 git init
 ```

**Conectando github/gitlab com SSH**
- [github](https://help.github.com/pt/github/authenticating-to-github/connecting-to-github-with-ssh)
- gitlab

**Linkar projeto com o criando no github/gitlab** 
```
git remote add origin https://github.com/user/repo.git.
```
```
git remote -v
```

**Se necessário não fazer uploads de arquivos ou diretórios no github/gitlab**
```
.gitignore 
```

**Upload do projeto**
```
git add .
```

**Criando commit inicial** 
```
git commit -m "my first commit"
``` 
**Publicando projeto local junto com todos os commits e objetos internos**
```
git push -u origin master
```

## Logs
```
git log
git log --decorate
git log --author="same_author"
```

**Visualizar autores**
```
git shortlog
git shortlog -sn
```
**Visualizar mudanças**
```
git log --graph
```

```
git show examplehash3239j423f34230482340a
git diff
```
**Reseta o arquivo antes de editar**
```
git checkout filename
```
**Reseta para antes de ter usado o comando `git add`**
```
git reset HEAD filename
```

## Branch

**Criando branch**
```
git checkout -b "Branch01"
```

**Ver branchs**
```
git branch
```

**Deletar uma branch**
```
git branch -D "Branch02"
```

### União de branchs
**Merge**
```
git merge branch_name
```
Commits são registrados em forma de ciclos para sequênciar mudanças registradas.

`git log --graph` para visulizar mudanças.

**Rebase**
```
git rebase branch_name
```
Commits são registrados de maneira linear.


## Operando commits

**Git stash**
```
git stash
git stash apply
git stash list
```
Cria estados WIP para guardar commits que poderão ser aplicados posteriormente
Stashes não são transferidos para o servidor quando você envia por push..

**Git revert**
```
git revert examplehash3239j423f34230482340a
```
Para reveter commits que gerou problemas em produção. Nao perde as mudanças como no comando `git reset`.


## Outros comandos
**Alias**
```
git config --global alias.sx status
git sx
```
sx passa a ser o alias para o comando `git status`.

**Git Tag**
```
git tag -a "anotação" -m "descrição da tag"
git push origin master --tags
git tag -d tagname
git push origin : name_tag or branch_name
```
