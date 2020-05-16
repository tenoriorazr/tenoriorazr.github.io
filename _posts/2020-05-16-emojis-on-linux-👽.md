---
layout: post
title:  "Notes on emojis and linux 👽"
date:   2020-05-16 02:40:00 -0300
categories: [linux, scripts]
---
### Emojis with version minimum Ubuntu installation + Openbox 

I wanted to print emojis on tty Linux, but it wasn't possible. At the moment, what know is some things about unicode, fonts and unicode code point.

and printed emojis in bash after starting startx with:

- Any [list](https://unicode.org/emoji/charts/full-emoji-list.html) of emojis
- Noto Color Emoji package installed (I believe it's for color output)
- printf and echo commands with unicode code point or Octal Escape Sequence

the result was...

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

Next steps: more information in forums or documentation to do update this post. Logs and scripts will no longer be the same.
