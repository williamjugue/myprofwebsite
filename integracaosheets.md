
---
layout: default
title: "Integração Google Sheets - Python"
permalink: /integracaosheets/
---

Clique aqui para voltar para a página anterior <a href="{{ '/PythonProjects/' | relative_url }}">Projetos Python</a>

## Aqui, vamos mostrar um passo a passo de como linkar o Python com o Google Sheets:

> Passo 1: Ativar na página do Google Developer Console o link com a API

<img src="{{ '/assets/imagesgooglesheet/passo1.png' | relative_url }}" alt="Google Developer Console" height="200">

Na primeira vez que entrar, deve aceitar os termos de uso da plataforma.

> Passo 2: Clicar em **Selecionar um projeto** e criar Novo Projeto

<img src="{{ '/assets/imagesgooglesheet/passo2.png' | relative_url }}" alt="Criar novo projeto" height="250">
<img src="{{ '/assets/imagesgooglesheet/passo2_5.png' | relative_url }}" alt="Criar novo projeto2" height="250">

> Passo 3: Ativar as APIs do Google Drive e Google Sheets.

Na barra de pesquisa, digitar "Google Drive API" e "Google Sheets API" e ativá-las

<img src="{{ '/assets/imagesgooglesheet/passo3_1.png' | relative_url }}" alt="Google Docs" height="250">
<img src="{{ '/assets/imagesgooglesheet/passo3_2.png' | relative_url }}" alt="Google Sheets" height="250">

> Passo 4: Nas 3 barras horizontais, ao lado do "Google Cloud", acessar "API e serviços" -> "API e serviços ativados"
<img src="{{ '/assets/imagesgooglesheet/passo4.png' | relative_url }}" alt="API e serviços" height="250">

Ir em "Tela de permissão OAuth" para configurar a autenticação
<img src="{{ '/assets/imagesgooglesheet/passo4_2.png' | relative_url }}" alt="OAuth" height="250">

E começar a configurar as permissões

> Passo 5: Preencher os dados de nome do projeto e email de notificação. Após preencher os 4 passos, apertar o botão "Criar".

> Passo 6: Configurar os usuários teste. Ir na aba "Público-alvo".

<img src="{{ '/assets/imagesgooglesheet/passo6.png' | relative_url }}" alt="Público alvo" height="150">

Preencha os emails dos usuários teste.

> Passo 7: Configurar os clientes do aplicativo (usuários) -> Criar ID do cliente do OAuth

<img src="{{ '/assets/imagesgooglesheet/passo7.png' | relative_url }}" alt="Credenciais" height="250">

Preencher o tipo de aplicativo "App para computador" e dar um nome à sua credencial.

Com a credencial criada, guardar a chave secreta ou baixar o arquivo JSON. Você pode editar o nome do arquivo para ficar mais facil de importar no Python quando fizermos a integração Python-API

> Passo 8: Em posse do ID do cliente OAuth, colocar agora as credenciais na pasta do código Python. Vamos abrir a documentação da API do Google Sheets no Python.

<img src="{{ '/assets/imagesgooglesheet/passo8.png' | relative_url }}" alt="API Python" height="250">

Na documentação, devemos instalar na sua distribuição Python a API do Google Sheets

'''
    python3 -m pip install --upgrade google-api-python-client google-auth-httplib2 google-auth-oauthlib
'''

Agora, terminamos a configuração. Podemos rodar um exemplo:

> Passo 9: Crie uma planilha Google. Copie o ID da planilha, que está entre duas barras / / 
<img src="{{ '/assets/imagesgooglesheet/passo9.png' | relative_url }}" alt="Id planilha" height="250">


> Passo 10: Rode o exemplo de amostra da documentação. No caso, vamos logar no aplicativo. Copie o código exemplo e edite:

1. SCOPES = ["https://www.googleapis.com/auth/spreadsheets.readonly"] -> Apagar o .readonly
2. Editar o ID na linha SAMPLE_SPREADSHEET_ID = "1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms" para o que foi copiado no passo 9.
3. Editar o intervalo a ser trabalho. No meu caso, criei uma planilha Página1 que vai da célula A1 até B13
    SAMPLE_RANGE_NAME = "Página1!A1:B13"




'''
    import os.path

    from google.auth.transport.requests import Request
    from google.oauth2.credentials import Credentials
    from google_auth_oauthlib.flow import InstalledAppFlow
    from googleapiclient.discovery import build
    from googleapiclient.errors import HttpError

        # Se for editar, apagar .readonly
    SCOPES = ["https://www.googleapis.com/auth/spreadsheets"] 

        # O ID da planilha obtido no link do navegador

    SAMPLE_SPREADSHEET_ID = "1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms"

        #Intervalo da planilha "Página1" com intervalo de trabalho A1:B13

    SAMPLE_RANGE_NAME = "Página1!A1:B13"

        # função principal de edição da planilha
    def main():
    """ Shows basic usage of the Sheets API.
    Prints values from a sample spreadsheet.
    """
        creds = None

        # Se existir token, passa

        if os.path.exists("token.json"):
            creds = Credentials.from_authorized_user_file("token.json", SCOPES)

        # Sem credenciais válidas, fazer login
        if not creds or not creds.valid:
            if creds and creds.expired and creds.refresh_token:
            creds.refresh(Request())
            else:
            flow = InstalledAppFlow.from_client_secrets_file(
                "credentials.json", SCOPES
            )
            creds = flow.run_local_server(port=0)
            # Save the credentials for the next run
            with open("token.json", "w") as token:
            token.write(creds.to_json())

        try:
            service = build("sheets", "v4", credentials=creds)

            # Call the Sheets API
            sheet = service.spreadsheets()
            result = (
                sheet.values()
                .get(spreadsheetId=SAMPLE_SPREADSHEET_ID, range=SAMPLE_RANGE_NAME)
                .execute()
            )
            print(result)
        except HttpError as err:
            print(err)

    if __name__ == "__main__":
        main()

'''

> Passo 11: Execute o código e faça login. Aceite as permissões.

<img src="{{ '/assets/imagesgooglesheet/passo11.png' | relative_url }}" alt="Login" height="250">

O output do seu código deve ser algo assim:

<img src="{{ '/assets/imagesgooglesheet/passo11_2.png' | relative_url }}" alt="Output1" height="150">

Temos um dicionário com chaves e valores como lista de listas Python.

> Passo 12: Adicionar uma informação em outra célula. Vamos adicionar na célula A14 a informação "Janeiro2"

1. Vamos copiar o código result e editar para fazer um update       
'''
    result = (
                sheet.values()
                .get(spreadsheetId=SAMPLE_SPREADSHEET_ID, range=SAMPLE_RANGE_NAME)
                .execute()
            )
'''

tornar-se-á

2. 

'''
    result = sheet.values().update(spreadsheetId=SAMPLE_SPREADSHEET_ID,
                                    range="A14",valueInputOption="USER_ENTERED",
                                    body={'values': adicionar_valores}).execute()
'''

com get => update, range => "A14";

3. Adicionando os seguintes parâmetros
valueInputOption="RAW" ou "USER_ENTERED" , se você quiser o input literal string (RAW) ou como o usuário inseriria na planilha no aplicativo "USER_ENTERED"
body={'values': adicionar_valores}, sendo adicionar_valores *definido antes de result* como a lista da lista das variáveis que você quer adicionar.

'''
    adicionar_valores = [
        ["Janeiro1"],
    ]
'''

Dessa forma, temos o seguinte resultado

<img src="{{ '/assets/imagesgooglesheet/passo12.png' | relative_url }}" alt="janeiro2" height="250">

4. Para adicionar mais de uma informação, vamos acrescentar mais células
'''
    adicionar_valores = [
        ["Janeiro2", "R$ 250000,00"],
        ["Fevereiro2","R$ 3002,50"],
    ]
'''

<img src="{{ '/assets/imagesgooglesheet/passo12_2.png' | relative_url }}" alt="fevereiro2" height="250">

> Passo 13: Podemos fazer um loop para preencher várias células de uma só vez. 

1. Vamos usar os dados de Janeiro2 e Fevereiro2. Para isso, alteraremos o intervalo de trabalho do GET para A1:B15
SAMPLE_RANGE_NAME = "Página1!A1:B15"

2. Vamos pegar uma lista com apenas os valores da variável result do GET.
valores = result['values']

3. Definimos a coluna "Imposto" em C1 com:

adicionar_valores = [
            ["Imposto"],
        ]

4. Criamos o loop for para percorrer todas as linhas e calcular o imposto. Note que precisamos transformar o valor em moeda para número puro do Python com a função REPLACE. Depois escrevemos na planilha com o formato
'''
for i, linha in enumerate(valores):
    if i > 0: #pula o cabeçalho
        vendas = linha[1] 
        vendas = vendas.replace("R$ ","").replace(".","") #Retira R$ e tira o ponto separador de milhar
        vendas = float(vendas.replace(",",".")) #transforma , em ponto (notação americana) e transforma em número racional
        imposto = vendas*0.2
        imposto = f'R$ {imposto:.2f}'.replace(".",",") #transforma em moeda no padrao brasileiro com 2 casas decimais
        adicionar_valores.append([imposto]) #cria uma nova linha a cada lista
'''

5. Colocamos **fora do loop FOR** a ação de atualizar a planilha, colocando o range em C1
'''
    result = sheet.values().update(spreadsheetId=SAMPLE_SPREADSHEET_ID,
                            range="C1",valueInputOption="USER_ENTERED",
                            body={'values': adicionar_valores}).execute()
'''

Aqui está o resultado final
<img src="{{ '/assets/imagesgooglesheet/passo13.png' | relative_url }}" alt="Loop FOR" height="250">

