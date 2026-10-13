---
layout: default
title: "Meus projetos em Python"
permalink: /pythonprojects/
---

# Tipo de projetos que estudo
## Python
1. Gerador de QR Code
Para instalar no seu computador um gerador de QR code a partir de um link, vamos precisar de duas extensões do Python: qrcode e Pillow.
Essas extensões podem ser instaladas via pip
```
    pip install qrcode
    pip install Pillow

```
ou via conda, substituindo **pip** por **conda**.

Para gerar um código simples, podemos fazer o seguinte:
```
    import qrcode

    imagem = qrcode.make("https://williamjugue.github.io/myprofwebsite/about/")
    imagem.save("QRCode1.png")
```

2. API de cotação de moedas em tempo real

Neste caso, coletamos a cotação do dólar na data de hoje.

```

    import requests
    import json
    cotacoes = requests.get('https://economia.awesomeapi.com.br/json/all') #usa API de moedas
    cotacoes_dic = cotacoes.json() #converte para dicionario python

    cotacoes_dolar = cotacoes_dic['USD']['bid'] #coleta o valor da oferta de compra do dólar de hoje
    print(f'Dólar: R$ {cotacoes_dolar}')

```

3. É possível coletar dados ao longo de um determinado período de tempo e colocar num gráfico

```
    import requests
    import json
    cotacoes = requests.get('https://economia.awesomeapi.com.br/json/daily/USD-BRL/30') #importa os ultimos 30 dias
    cotacoes_dic = cotacoes.json()

    cotacoes_dolar = [float(dolardia['bid']) for dolardia in cotacoes_dic] #cria lista com os valores dos ultimos 30 dias
    cotacoes_dolar.reverse() #troca a ordem, que era do ultimo para o primeiro, para primeiro em direcao ao ultimo

    import matplotlib.pyplot as plt
    import numpy as np

    #dias = np.arange(30) #30 dias
    grafico = plt.plot(cotacoes_dolar)
    plt.xlabel("Últimos 30 Dias")
    plt.ylabel("Valor do USD em BRL")
    plt.show()
```

Aqui está um exemplo de gráfico rudimentar gerado com os últimos 30 dias de cotação do dólar americano. Observe que o valor mais à direita é o valor atual.

<img src="{{ '/assets/images/graficodolar.png' | relative_url }}" alt="Cotação últimos 30 dias dolar" height="450">


4. Para ver um tutorial detalhado sobre como fazer integração Python - Google Planilhas, deixo o link abaixo
<a href="{{ '/integracaosheets/' | relative_url }}">Integração</a>