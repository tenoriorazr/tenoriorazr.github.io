---
layout: post
title:  "Notes on Docker 01"
date:   2020-05-14 04:30:00 -0300
categories: [docker]
---
## The docker commit command in use to create images from a container.

### Create image
```docker commmit 3b45rbid123 imagemx:versao01```

### Distributing image "na mão" via tar package
```docker save imagem:versao01 > /tmp/minha-imagem.tar```

### Import image
```docker load < minha-imagem.tar```
