---
layout: post
title:  "Notas sobre emojis no bash 👽"
date:   2020-05-16 02:40:00 -0300
categories: [linux, scripts]
---

_"A vida é feita de escolhas e nesse momento escolho sair." - Nelson Teich._

---

Imaginei executar scripts com emojis indicando alguma coisa, nada além de uma saída diferenciada durante a execução.

obs.: Não é possível exibir emojis no tty. 

Iniciei startx e no bash exibi as famosas carinhas tendo em mãos:

- Qualquer [lista](https://unicode.org/emoji/charts/full-emoji-list.html) de emojis
- Pacote _Noto Color Emoji_ instalado (Para exibir colorido)
- Comandos `printf` e `echo` com algum código unicode e/ou Sequências de escape.


Resultado:

```
# printf '\U1F47D\n'
👽
# printf '\360\237\221\275\n'
👽
```
ou
```
# echo $'\360\237\221\275'
👽
# echo $'\U1F47D'
👽
 ```
![thatsallfolks](https://qph.fs.quoracdn.net/main-qimg-0091a2fc16180ba9a3b0b0e74678ca1f)

