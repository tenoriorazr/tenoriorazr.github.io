---
layout: post
title:  "Notas sobre como fazer solicitações à API's por linha de comando via cURL"
date:   2021-01-20 08:30:00 -0300
categories: [linux, shell script, bash]
---

## Como fazer solicitações à API's por linha de comando via cURL.

### Objetivo
Demonstração de como fazer transferência de dados via URL com soliticações GET, POST, PUT, PATCH, e DELETE via cURL.

## Endpoints
É possível testar chamadas de API com dados fakes, um exemplo de site para consultas é o [JSON Placeholder](https://jsonplaceholder.typicode.com/).

**/posts** significa uma consulta de todos os posts, e o **1** de **/posts/1** representa **/posts/{id}**, logo *ID número 1*.

Métodos/Verbos para endpoints:

|Método || Endpoint                                       |
|:------|-|:---------------------------------------------:|
|GET    || <https://jsonplaceholder.typicode.com/posts>   |
|POST   || <https://jsonplaceholder.typicode.com/posts>   |
|PUT    || <https://jsonplaceholder.typicode.com/posts/1> |
|PATCH  || <https://jsonplaceholder.typicode.com/posts/1> |
|DELETE || <https://jsonplaceholder.typicode.com/posts/1> |


## cURL CLI

- `-X --request` - Método request
- `-d --data` - Envia os dados especificados
- `-H --header` - Envia headers
- `-i --include` - Exibe respostas dos headers

### GET
Obtém dados.

**GET REQUEST**
```bash
👽@🐧:~$ curl https://jsonplaceholder.typicode.com/posts
```
> `curl -i` para obter mais informações dos headers.

### POST
Cria um novo recurso. Não é *non-idempotent*, o que significa que duas solicitações POST idênticas criarão dois novos recursos. 

**POST Request**
```bash
👽@🐧:~$ curl -X POST -d "userId=5&title=Um titulo qualquer&body=Um maravilhoso guia diga-se de passagem." https://jsonplaceholder.typicode.com/posts
```

**POST Request (json)**
```bash
👽@🐧:~$ curl -X POST -H "Content-Type: application/json" -d '{"userId": 5, "title": "Um titulo qualquer", "body": "Um maravilhoso guia diga-se de passagem."}' https://jsonplaceholder.typicode.com/posts
```

### PUT
Atualiza um recurso existente. É *idempotent*, o que significa que duas solicitações PUT idênticas modificarão o mesmo recurso. 
Uma solicitação PUT requer que todo o corpo seja enviado; se algum dado estiver faltando, esses dados serão apagados (exceto valores automáticos como IDs de incremento automático, ID's e timestamps). 

**PUT Request**
```bash
👽@🐧:~$ curl -X PUT -d "userId=1&title=Outro titulo&body=Um novo body" https://jsonplaceholder.typicode.com/posts/1
```

**PUT Request (json)**
```bash
👽@🐧:~$ curl -X PUT -H "Content-Type: application/json" -d '{"userId": 1, "title": "Outro titulo", "body": "Um novo body"}' https://jsonplaceholder.typicode.com/posts/1
```

### PATCH
Atualiza um recurso existente e não requer o envio de todo o corpo com a solicitação. 

**PATCH Request**
```bash
#PATCH Request
👽@🐧:~$ curl -X PATCH -d "title='Mude so o titulo'" https://jsonplaceholder.typicode.com/posts/1
```

**PATCH Request (json)**
```bash
👽@🐧:~$ curl -X PATCH -H "Content-Type: application/json" -d '{"title": "Mude so o titulo"}' https://jsonplaceholder.typicode.com/posts/1
```

### DELETE
DELETE remove um recurso.

**DELETE Request**
```bash
👽@🐧:~$ curl -X DELETE https://jsonplaceholder.typicode.com/posts/1
```

### Autenticação
Se for preciso enviar headers adicionais, como `Authorization: Bearer` ou `x-jwt-assertion` para autenticação baseada em JWT, pode ser feito desta forma:

```bash
👽@🐧:~$ curl \
   -H "Content-Type: application/json" \
   -H "Authorization: Bearer <JWT_TOKEN>"" \
   -H "x-jwt-assertion: <JWT_TOKEN>" \
   -X POST \
   -d '{"chave1": "valor1", "chave2": "valor2"}' \
   https://exemplo.com/
```

## Conclusão
Taí um guia básico para começar a testar APIs via cURL usando JSON ou dados de formulário codificados por url(urlencoded form data).
