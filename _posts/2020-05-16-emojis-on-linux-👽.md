---
layout: post
title:  "Notas sobre emojis no bash 👽"
date:   2020-05-16 02:40:00 -0300
categories: [linux, scripts]
---

_"A vida é feita de escolhas e nesse momento escolho sair." - Nelson Teich._

&nbsp;
Imaginei rodar scripts e ver emojis indicando alguma coisa na tela, nada além de uma saída divertida durante a execução.
Eu queria exibir emojis no tty, mas não foi possível. 

Iniciei startx e no bash exibi as famosas carinhas tendo em mãos:

- Qualquer [lista](https://unicode.org/emoji/charts/full-emoji-list.html)
- Pacote Noto Color Emoji package instalado (Para exibir colorido)
- printf e/ou echo com algum código unicode e Sequência de escape.

&nbsp;
E esse tem sido o resultado:

```
# printf '\U1F47D\n'
👽
# printf '\360\237\221\275\n'
👽
```
or
```
# echo $'\360\237\221\275'
👽
# echo $'\U1F47D'
👽
 ```
![thatsallfolks](https://qph.fs.quoracdn.net/main-qimg-0091a2fc16180ba9a3b0b0e74678ca1f)

