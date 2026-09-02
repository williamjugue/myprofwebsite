---
layout: default
title: "Meus projetos"
permalink: /projects/
---

# Tipo de projetos que estudo
## Python
### Gerador de QR Code
Para instalar no seu computador um gerador de QR code a partir de um link, vamos precisar de duas extensões do Python: qrcode e Pillow.
Essas extensões podem ser instaladas via pip
```
    pip install qrcode
    pip install Pillow

```
ou via conda, substituindo **pip** por **conda**
Para gerar um código simples, podemos fazer o seguinte:
```
    import qrcode

    imagem = qrcode.make("https://williamjugue.github.io/myprofwebsite/about/")
    imagem.save("QRCode1.png")
```