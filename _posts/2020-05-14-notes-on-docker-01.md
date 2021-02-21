---
layout: post
title:  "Notes sobre Docker"
date:   2020-05-14 04:30:00 -0300
categories: [docker, bash, linux]
---

## 🐋 O básico do Docker
A proposta desse guia é apresentar os conceitos mais básicos do docker para utilização na real ou didático.

#### **Comandos**
#### Iniciando um novo container
`--name`: associa um nome para o container, `-v`: volume, `-d`: o container funciona em modo background, `sh -c` para instalar alguma coisa via shell. 
```bash
🐋@🐧:~$ docker run --name [nome do container] -v [/host/volume/local]:[/container/armazenaraqui] --network [rede_exemplo] -p [host_ip]:[host_port]:[container_port] -d [nome da imagem, ex.: node:14.15-alpine3.10] sh -c "yarn install && yarn run dev"
```
> Saber mais sobre [docker run](https://docs.docker.com/engine/reference/commandline/run/)

> <sub>Dica: basicamente é o processo mais rápido e bagunçado para iniciar um container, uma alternativa melhor para isso é subir o container com docker-compose.</sub>

#### Acessando o container
`-ti` para modo interativo, `-t` é do tty e `i` de interactive, mantém o STandarD INput aberto. `/bin/bash` se o container tiver o bash instalado.
```bash
🐋@🐧:~$ docker exec -ti [id ou nome do container] /bin/bash
```

#### Listando containers executados e parados. list all containers
```bash
🐋@🐧:~$ docker ps -a
```

#### Listando as configurações de rede
```bash
🐋@🐧:~$ docker network ls
```
> Saber mais sobre [docker network](https://docs.docker.com/network/)

#### Apagando um configuração de rede
```bash
🐋@🐧:~$ docker network rm [id que representa a rede, ex.: usuario_default]
```

#### Parando o container
```bash
🐋@🐧:~$ docker stop [id ou nome do container]
```

#### Apagando o container
```bash
🐋@🐧:~$ docker rm [id ou nome do container]
```

#### Apagando a imagem
```bash
🐋@🐧:~$ docker rmi [id ou nome da imagem]
```

#### Criando a imagem de um container existente
```bash
🐋@🐧:~$ docker commmit [id do container] imagemx:versao01
```

#### Salvando imagem em um arquivo .tar
```bash
🐋@🐧:~$ docker save imagem:versao01 > /tmp/minha-imagem.tar
```

#### Importando imagem de um arquivo .tar
```bash
🐋@🐧:~$ docker load < minha-imagem.tar
```

## Docker compose
Basicamente o arquivo `docker-compose.yml` é isso:
```yml
version: '3.7'
services:
  [nome do serviço]:
    image: [nome da imagem]
    container_name: 'nome do container'
    restart: always
    ports:
      - "5000:5000"
    volumes:
      - pastalocaldelogs:/var/log
    environment:
        Váriavelpadrão: "${VARIAVEL VINDO DO ARQUIVO .env}"
        OutraVáriavelpadrão: "${OUTRA VARIAVEL VINDO DO ARQUIVO .env}"
```

**Subindo container via docker-compose**
```bash
🐋@🐧:~$ docker-compose up -d
```
Saber mais sobre [docker-compose](https://docs.docker.com/get-started/08_using_compose/)

## Dockerfile
Basicamente o arquivo `Dockerfile` é isso:

- ```FROM``` - Cria uma camada da imagem Docker.
- ```COPY``` - Copia arquivos do Docker client local.
- ```RUN``` - Uma forma de shell, o comando é executado em um shell, que por padrão é /bin/sh -c no Linux ou cmd/S/C no Windows). ```RUN [" executável "," parametro1 "," parametro2 "]``` (exec) A instrução executará quaisquer comandos em uma nova layer sobre a imagem atual e commita os resultados. A imagem commitada será usada na próxima etapa do Dockerfile.
- ```CMD``` - Especifica o comando a ser executado no contêiner.

> Boas práticas para escrever Dockerfiles: [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

## docker-compose e Dockerfile
Um projeto em diretório local configurado para ser *conteinerizado* via DOCKERFILE sendo executado via docker-compose.

**Dockerfile**
```
FROM node:14.15-alpine3.10
COPY . /home/projetox
RUN cd /app
CMD npm run dev
```

**docker-compose.yml**
```yml
version: '3.7'
services:
  app:
    build: .
    container_name: 'appweb-semdb'
    restart: always
    ports:
      - "5000:5000"
```

## Conclusão
Parece simples 😂. Com esse guia é possível ver que o docker é um aliado poderoso para estudos e trabalho sempre que for preciso trabalhar com containers virtualizando geral.
Através da documentação oficial é possível entender mais do Docker e consequentemente aprender muitos assuntos como shell, rede e segurança.
