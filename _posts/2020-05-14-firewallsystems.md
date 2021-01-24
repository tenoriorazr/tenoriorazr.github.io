---
layout: post
title:  "Notas sobre Sistemas de Firewall"
date:   2020-05-06 06:30:00 -0300
categories: [security, server]
---

_"O político só tem dois pensamentos, ou você é instrumento ou você é adversário." - Emílio Surita._
---

[![Firewall](https://image.flaticon.com/icons/png/128/2059/2059030.png)](https://blog.evttenorio.com/security/server/2020/05/06/sysfirewalls.html)

## Conceitos básicos
Sistemas de firewalls se desajustados podem causar interferências indesejadas no tráfego.

  - Hosts in line ou nível de circuito
  - DMZ
  - Desagrupamento de serviços em máquinas
  
Firewall Systems description by Oracle docs: [Link](https://docs.oracle.com/cd/E19253-01/816-4557/concept-25/index.html)

### Hosts in-line ou em nível de circuito

Conceito fundamental para quem opera ou analisa sistemas de firewall. É quando um host possui dois ou mais adaptadores e está posicionado no caminho de um tráfego. Dados passam por esse host. Exemplos de hosts que estarão sempre in-line: Bridges e Roteadores.

> Bridges são essenciais em sistema de firewalls pois são invisíveis para análises remotas da topologia, permitem implementações transparentes de elementos de firewall via camada de Enlace (2 - Modelo OSI / Capítulo 12).

### DMZ

***Demilitarized zone***. Rede separada da rede principal para reunir servidores que terão contato com quaisquer outras redes externas. Visitantes oriundos da internet ou de redes estranhas na mesma organização deverão ter acesso apenas à DMZ.
Em caso de intrusão o invasor deverá ficar contido na DMZ, sem possibilidade de sair.

### Desagrupamento de serviços em máquinas

**Todo serviço de rede possuem falhas de seguranças**. O objetivo é instalar apenas um serviço por máquina. O desagrupamento de serviços será essencial para a implementação da *defesa em profundidade em sistemas de firewall*. 

> Instalar um serviço por máquina através da virtualização. Atentar com segurança para a escolha da virtualização para que o isolamento da mesma não sobressaia para a máquina física.


## Sistemas de Firewall
**Firewall é um conceito.** 

  - Firewall não é uma máquina, é qualquer esforço físico, lógico e recursos empregados para prover e empregar segurança a uma rede de computadores. Humanos são recursos que também fazem parte de um sistema de firewall, Interage com as camadas 2 a 7.
  - Todo o tráfego destinado a servidores de rede ou áreas sensíveis da rede deverá passar através do firewall.
  - O sistema de firewall funciona com base em observação e/ou ação, havendo sempre, nesse último caso, autorização ou negação de passagem, definidos pela política de segurança. Em outras palavras, pode-se ter sensores passivos, que apenas verão o que trafega e emitirão alertas oportunos; elementos ativos que bloquearão o tráfego malicioso, quando for o caso.
  - O sistema de firewall deverá ser composto de diversos elementos.
  - O sistema de firewall deverá ser imune à invasão.
  
> **Atenção!** IPTABLES não é firewall.

### Netfilter - Filtro de Pacotes
Netfilter é um elemento de firewall atuante na rede que pode bloquear ou manipular tipos de tráfegos. O ```iptables``` é o comando que manipula o netfilter.

Netfilter entende as camadas 3 e 4 - OSI, manipulando recursos dos protocolos dessas camadas.

## Defesa em profundidade

Deve-se usar dois elementos de firewall em uma máquina se não houver alternativa. Exemplo de caso: Implementação do Proxy transparente, quando deverá existir um proxu e um filtro de pacotes para fazer desvio de porta.

## Elementos de Firewall
Elementos de Firewall é um recurso que faz algum tipo de análise, registro e/ou bloqueio. Atua nas camadas 2, 3, 4 e 7, poderá haver atuação nas camadas 5 e 6.

### Filtro de pacotes
- Filtro de pacotes não analisa a camada 7.
- São capazes de realizar NAT.
- Se o netfilter estiver presente em uma máquina intermediária entre hosts ou redes, essa máquina deverá realizar roteamento de rede.
- Podem entender elementos da camada 2, como endereço MAC
- São como guardas de transito que permitem a passagem de carros(pacotes) que satisfaçam pré-requisitos, como direção do tráfego.

Sobre [Iptables](https://blog.evttenorio.com/)

### Filtro de estados
Analisam estados das conexões e permitem que o tráfego, alem de direção tenha sentido.
Exemplo de estados utilizados pelo netfilter do kernel Linux:
- ```NEW``` - relativo a pacotes que estabelecem uma nova conexão ou associados a uma conexão que não possui pacotes transitando previamente em ambas direções
- ```ESTABLISHED``` - atribuído a tráfego associado com uma conexão sobre a qual há pacotes transitando em todas as direções (exceto o primeiro de todos, que se enquandrará como NEW)
- ```RELATED``` - relativo a um pacote que está iniciando uma conexão, mas econtra-se associado a uma outra já existente. Exemplo: mecanismo de transferencia (porta 20) e autenticação (porta 21) do FTP.
- ```INVALID``` - referente a pacotes que não podem ser identificados por algum motivo, incluindo os que provocarem vazamentos ou violação de memória e erros ICMP que não correspondam a nenhuma conexão previamente conhecida.

### Filtro de enlace
- Atuam na camada 2.
- Trata de endereços MAC, Tráfego VLANs e entre outros itens correlatos.
- Similares ao filtro de pacotes.
- ebtables.
```
ebtables -A FORWARD -s 01:02:03:04:a1:06 -p IPV4 -j ACCEPT
ebtables -A FORWARD -s 01:02:03:04:a1:06 -j DROP
```

### Proxies
- Elemento intermediário e que atua como cliente e servidor.
- Atuam diretamente na camada 7, entendem a camada 3 para selecionar o tráfego-alvo.
- Existem proxies para HTTP, FTP, SMTP, DNS, etc.
- Proxy não acelera a internet. Por ocasião de consulta a sites, os caches são responsáveis pela aceleração. Squid é um exemplo de proxy que oferece HTTP com cache.
- Forward Proxy: O cliente acessa vários servidores diferentes simultaneamente. Exemplo: Usuários de redes internas que precisam acessar sistes da Internet, nesse caso implementa-se um proxy HTTP de forward com cache.
- Reverse Proxy: Vários clientes precisam acessar um determinado servidor. O servidor de rede deve ter um servidor de proxy reverso a frente de clientes.

### [---]

### [---]

### [---]

### [---]

### [---]

### [---]
