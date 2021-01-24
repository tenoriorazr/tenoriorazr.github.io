---
layout: post
title:  "Notes sobre Docker"
date:   2020-05-14 04:30:00 -0300
categories: [docker]
---
---

## O básico do Docker
Comandos úteis do Docker para começar e/ou lembrar.


### Criando a imagem
Usando o comando docker commit para criar imagens de um container.
```docker commmit 3b45rbid123 imagemx:versao01```

### Salvando imagem em um arquivo comprimido
```docker save imagem:versao01 > /tmp/minha-imagem.tar```

### Importando imagem de um arquivo comprimido
```docker load < minha-imagem.tar```

## Dockerfile.

- ```FROM``` - Cria uma camada da imagem Docker.
- ```COPY``` - Copia arquivos do Docker client local.
- ```RUN``` - Uma forma de shell, o comando é executado em um shell, que por padrão é /bin/sh -c no Linux ou cmd/S/C no Windows). ```RUN [" executável "," parametro1 "," parametro2 "]``` (exec) A instrução executará quaisquer comandos em uma nova layer sobre a imagem atual e commita os resultados. A imagem commitada será usada na próxima etapa do Dockerfile.
- ```CMD``` - Especifica o comando a ser executado no contêiner.

Boas práticas para escrever Dockerfiles: [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
