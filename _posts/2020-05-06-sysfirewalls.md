---
layout: post
title:  "Sistemas de Firewall"
date:   2020-05-06 04:40:00 -0300
categories: [security]
---

# Capítulo 17
## Sistemas de Firewall
[![N|Solidx](https://cldup.com/dTxpPi9lDf.thumb.png)](https://google.com)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://blog.evttenorio.com)

## 17.1 Conceitos básicos em sistemas de firewall
Sistemas de firewalls se desajustados podem causar interferências indesejadas no tráfego.

  - Hosts in line ou nível de circuito
  - DMZ
  - Desagrupamento de serviços em máquinas

### Hosts in-line ou em nível de circuito

Conceito fundamental para quem opera ou analisa sistemas de firewall. É quando um host possui dois ou mais adaptadores e está posicionado no caminho de um tráfego. Dados passam por esse host. Exemplos de hosts que estarão sempre in-line: Bridges e Roteadores.

> Bridges são essenciais em sistema de firewalls pois são invisíveis para análises remotas da topologia, permitem implementações transparentes de elementos de firewall via camada de Enlace (2 - Modelo OSI / Capítulo 12).

### DMZ

***Demilitarized zone***. Rede separada da rede principal para reunir servidores que terão contato com quaisquer outras redes externas. Visitantes oriundos da internet ou de redes estranhas na mesma organização deverão ter acesso apenas à DMZ.
Em caso de intrusão o invasor deverá ficar contido na DMZ, sem possibilidade de sair.

### Desagrupamento de serviçoes em máquinas

**Todo serviço de rede possuem falhas de seguranças**. O objetivo aqui é instalar apenas um serviço por máquina. O desagrupamento de serviços será essencial para a implementação da *defesa em profundidade em sistemas de firewall*. 

> Instalar um serviço por máquina através da virtualização. Atentar com segurança para a escolha da virtualização para que o isolamento da mesma não sobressaia para a máquina física.


# 17.2 Sistemas de Firewall
**Firewall é um conceito.** 

  - Firewall não é uma máquina, é qualquer esforço físico, lógico e recursos empregados para prover e empregar segurança a uma rede de computadores. Humanos são recursos que também fazem parte de um sistema de firewall.
  - Todo o tráfego destinado a servidores de rede ou áreas sensíveis da rede deverá passar através do firewall.
  - O sistema de firewall funciona com base em observação e/ou ação, havendo sempre, nesse último caso, autorização ou negação de passagem, definidos pela política de segurança. Em outras palavras, pode-se ter sensores passivos, que apenas verão o que trafega e emitirão alertas oportunos; elementos ativos que bloquearão o tráfego malicioso, quando for o caso.
  - O sistema de firewall deverá ser imune à invasão.
  
> **Atenção!** Se você usa Linux o seu firewall não é IPTABLES!
