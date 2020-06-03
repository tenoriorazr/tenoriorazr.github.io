---
layout: post
title:  "Notes on git"
date:   2020-06-03 08:30:00 -0300
categories: [git]
---

[EM MANUTENÇÃO]

Explicações com comandos úteis do git.
Útil para utilizar git com github ou gitlab.

**First, go to github/gitlab and create repository.** 
- Create a New Repository/Project. 
- Add name and description.

**Initial git configuration**
```
git config --global user.name "Myname"
git config --global user.mail "myemail@emails.com"
git config --global core.editor "Myname"
```

_Show configs_
```
git config --list
git config user.name
```

**Transforms current directory into git project and adds ".git"**
 ```
 git init
 ```

**Connecting to github/gitlab with SSH**
- github
- gitlab

**Link you project with repository on github/gitlab** 
```
git remote add origin https://github.com/user/repo.git.
```
```
git remote -v
```

**If necessary, not to upload files in github/gitlab**
```
.gitignore 
```

**Up files to github/gitlab.**
```
git add .
```

**Create a initial commit** 
```
git commit -m "my first commit"
``` 
**And after... push**
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

**Create branch**
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


## Operations commits

**Git stash**
```
git stash
git stash apply
git stash list
```
Cria estados WIP para guardar commits que poderão ser aplicados posteriormente

**Git revert**
```
git revert examplehash3239j423f34230482340a
```
Para reveter commits que gerou problemas em produção. Nao perde as mudanças como no comando `git reset`.


## Other commands
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
