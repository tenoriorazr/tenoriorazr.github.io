---
layout: post
title:  "Notes sobre Docker 01"
date:   2020-05-14 04:30:00 -0300
categories: [docker]
---
#### Usando o comando docker commit para criar imagens de um container.

### Criando a imagem
```docker commmit 3b45rbid123 imagemx:versao01```

### Salvando imagem em um arquivo comprimido
```docker save imagem:versao01 > /tmp/minha-imagem.tar```

### Importando imagem de um arquivo comprimido
```docker load < minha-imagem.tar```
