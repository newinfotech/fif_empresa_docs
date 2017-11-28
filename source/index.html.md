---
title: New Info Tech. FIF Empresa API

language_tabs:
  - shell
  - ruby
  - python

toc_footers:
  - <a href='https://newinfotech.com.br'>Entre em contato conosco para obter um Token de desenvolvedor</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Iniciando com a nossa API

Bem vindo(a) a documentação da nossa API, com essas informações você pode acessar os dados da sua empresa no nosso Banco de Dados, além de enviar e atualizar informações sobre suas cobranças nos nossos sistemas FIF (Ferramenta de Informação Financeira) e SIGF (Sistema Integrado de Gestão Financeira)

Os exemplos aqui descritos usam bibliotecas de Cliente HTTP de terceiros, para mais informações sobre essas bibliotecas, consulte a documentação oficial do desenvolvedor.
Os exemplos mostrados são das linguagens Shell (CURL), Ruby (rest-client), Python (requests),
 
> A raiz da API é: `https://newinfotech.com.br/api`

# Autenticação

> Use o seguinte código para autorizar o acesso a nossa API:

```ruby
require 'rest-client'

token = "<Seu token obtido na interface de empresa>"
api = RestClient::Resource.new "https://newinfotech.com.br/api", headers: {Authorization: token} 
```

```python
import requests

root = 'https://newinfotech.com.br/api'

req = requests.Session()
req.headers['Authorization'] = "<Seu token obtido na interface de empresa>"
```

```shell
# Em shell, só é necessário passar o cabeçalho correto
curl "endpoint_de_sua_escolha"
  -H "Authorization: <Seu token obtido na interface de empresa>"
```

> Subistitua `<Seu token obtido na interface de empresa>` com o Token obtido na página de [Configurações](https://newinfotech.com.br/empresas/#/config/integracao).

> Subistitua `endpoint_de_sua_escolha` pela Raiz + Endpoint o qual deseja acessar, Ex: `https://newinfotech.com.br/api/clientes`.

Nossa API usa Tokens para Autenticação e Autorização do usuário, para obter um token de acesso, visite suas [Configurações](https://newinfotech.com.br/empresas/#/config/integracao).

Para qualquer requisição autenticada a nossa API, o desenvolvedor deve usar o cabeçalho `Authorization` como abaixo:

`Authorization: Token c34no3y57y8n75y845t7vywbo7858tv7vmw8`

<aside class="notice">
Subistitua <code>Token c34no3y57y8n75y845t7vywbo7858tv7vmw8</code> pelo seu Token.
</aside>

# Clientes

## Obter todos os clientes

```ruby
require 'rest-client'
require 'json'

# ...
clientes = api['clientes/'].get
clientes = JSON.parse(clientes.body)
```

```python
import requests

# ...
req.get('{}/clientes'.format(root))
```

```shell
curl "https://newinfotech.com.br/api/clientes"
  -H "Authorization: <Seu token aqui>"
```


> O comando acima retornará o seguinte JSON:

```json
[{"id":43,
  "endereco":
   {"id":24,
    "cidade":"Arapiraca",
    "estado":"AL",
    "pais":"Brasil"},
  "email":"cliente@dominio.com",
  "cpf_cnpj":"000000000",
  "palavra_seguranca":"clienteps",
  "celular":"000000000",
  "nome_completo":"Cliente 1",
  "data_nascimento":"1993-06-14"}]

```

Este endpoint retorna todos os clientes vinculados a empresa.

### Requisição HTTP

`GET https://newinfotech.com.br/api/clientes`

### Parâmetros

<aside class="notice">
Este endpoint não aceita parâmetros adicionais
</aside>

## Obtendo um cliente específico

```ruby
require 'rest-client'
require 'json'

# ...
cliente = api['clientes/<cpf_do_cliente>'].get
cliente = JSON.parse cliente.body
```

```python
import requests

# ...
cliente = req.get('{}/clientes/<cpf_do_cliente>')
cliente = cliente.content
```

```shell
curl "https://newinfotech.com.br/api/clientes/<cpf_do_cliente>"
  -H "Authorization: <seu_token_aqui>"
```


> O comando acima retornará o seguinte JSON:

```json
{
  "id":43,
  "endereco":
   {"id":24,
    "cidade":"Arapiraca",
    "estado":"AL",
    "pais":"Brasil"},
  "email":"cliente@dominio.com",
  "cpf_cnpj":"000000000",
  "palavra_seguranca":"clienteps",
  "celular":"000000000",
  "nome_completo":"Cliente 1",
  "data_nascimento":"1993-06-14"
}
```

Este endpoint retorna um cliente específico

> Subistitua `<cpf_do_cliente>` pelo CPF/CNPJ do cliente que deseja obter

### Requisição HTTP

`GET https://newinfotech.com.br/api/clientes/<cpf_do_cliente>`

### URL Parameters

Parameter | Description
--------- | -----------
cpf_do_cliente | O CPF/CNPJ do cliente que se deseja obter


## Enviar uma lista de Clientes

```ruby
require 'rest-client'
require 'json'

# ...
# É necessário ser do tipo Array
clientes = [{
  cpf_cnpj: "00000000000",
  nome_completo: "Cliente 1",
  email: 'cliente@dominio.com',
  celular: '00000000000'
},{
  cpf_cnpj: "00000000001",
  nome_completo: "Cliente 2",
  email: 'cliente2@dominio.com',
  celular: '00000000001'
}
# ...
]
clientes = api['empresa/registrar_clientes/'].post JSON.generate(clientes), content_type: 'application/json'
clientes = JSON.parse(clientes.body)
```

```python
import requests

# ...
# É necessário ser do tipo list
clientes = [{
  'cpf_cnpj': "00000000000",
  'nome_completo': "Cliente 1",
  'email': 'cliente@dominio.com',
  'celular': '00000000000'
},{
  'cpf_cnpj': "00000000001",
  'nome_completo': "Cliente 2",
  'email': 'cliente2@dominio.com',
  'celular': '00000000001'
}
# ...
]

req.post('{}/empresa/registrar_clientes/', json=clientes)

```

```shell
curl "https://newinfotech.com.br/api/empresa/registrar_clientes/"
  -H "Authorization: <Seu token aqui>"
  -H "Content-Type: application/json"
  -X POST -d '[{"cpf_cnpj": "00000000000", "nome_completo': "Cliente 1","email": "cliente@dominio.com","celular": "00000000000","data_nascimento": "yyyy-mm-dd"},{"cpf_cnpj": "00000000001","nome_completo": "Cliente 2","email": "cliente2@dominio.com","celular": "00000000001","data_nascimento": "yyyy-mm-dd"}]'
```


> O comando acima retornará o seguinte JSON:

```json
{
  "status": "2 resgistros salvo(s) com sucesso", 
  "cont": 2
}
```

Use este endpoint para enviar uma lista de Clientes (Array) para o nosso sistema

<aside class="notice">
Observe se a contagem de itens na resposta corresponde à quantidade de itens enviados, caso não corresponda, pode ser que exista erro em algum item enviado
</aside>

### Requisição HTTP

`POST https://newinfotech.com.br/api/empresa/registrar_clientes/`

### Parâmetros

Parameter | Description
--------- | -----------
lista_de_clientes | Array com informações dos clientes a serem adicionados ao sistema

> Os dados necessários para o cadastro do Cliente estão listados no JSON abaixo:

```json
{
  "cpf_cnpj": "<cpf_cnpj_do_cliente>",
  "nome_completo": "<nome_do_cliente>",
  "email": "<email_do_cliente>",
  "celular": "<numero_de_celular_com_ddd>"
}
```

# Boletos

## Obtendo todos os boletos

```ruby
require 'rest-client'
require 'json'

# ...
boletos = api['boletos/'].get
boletos = JSON.parse(boletos.body)
```

```python
import requests

# ...
req.get('{}/boletos'.format(root))
```

```shell
curl "https://newinfotech.com.br/api/boletos"
  -H "Authorization: <Seu token aqui>"
```


> O comando acima retornará o seguinte JSON:

```json
[
  {"id":11514,
    "emissor":"Banco Bradesco S.A.",
    "cliente":"00000000000",
    "descricao":"",
    "valor":36.4,
    "data_vencimento":"2016-11-02",
    "pago":true,
    "create_datetime":"2017-04-04T04:01:39.885803Z",
    "write_datetime":"2017-04-08T00:23:25.009219Z",
    "boleto_url":"",
    "linha_digitavel":"23793380295020948930627006333309169660000003640",
    "baixa_manual":true,
    "despesa":null,
    "categoria":3}
]

```

Este endpoint retorna todos os boletos emitidos pela empresa.

### Requisição HTTP

`GET https://newinfotech.com.br/api/boletos`

### Parâmetros

<aside class="notice">
Este endpoint não aceita parâmetros adicionais
</aside>

## Obtendo um boleto específico

```ruby
require 'rest-client'
require 'json'

# ...
boleto = api['boletos/<id>'].get
boleto = JSON.parse boleto.body
```

```python
import requests

# ...
boleto = req.get('{}/boletos/<id>')
boleto = boleto.content
```

```shell
curl "https://newinfotech.com.br/api/boletos/<id>"
  -H "Authorization: <seu_token_aqui>"
```


> O comando acima retornará o seguinte JSON:

```json
{
    "id":11514,
    "emissor":"Banco Bradesco S.A.",
    "cliente":"00000000000",
    "descricao":"",
    "valor":36.4,
    "data_vencimento":"2016-11-02",
    "pago":true,
    "create_datetime":"2017-04-04T04:01:39.885803Z",
    "write_datetime":"2017-04-08T00:23:25.009219Z",
    "boleto_url":"",
    "linha_digitavel":"23793380295020948930627006333309169660000003640",
    "baixa_manual":true,
    "despesa":null,
    "categoria":3
}
```

Este endpoint retorna um boleto específico

> Subistitua `<id>` pelo ID do boleto que deseja obter

### Requisição HTTP

`GET https://newinfotech.com.br/api/boletos/<id>`

### URL Parameters

Parameter | Description
--------- | -----------
id | O `id` do boleto que se deseja obter


## Enviando uma lista de boletos

```ruby
require 'rest-client'
require 'json'

# ...
# É necessário ser do tipo Array
boletos = [{
  cliente: "00000000000",
  desricao: "Boleto 1",
  linha_digitavel: '000000000000000000000000000000000'
},{
  cliente: "00000000001",
  desricao: "Boleto 2",
  linha_digitavel: '000000000000000000000000000000001'
}
# ...
]
boletos = api['empresa/registrar_boletos/'].post JSON.generate(boletos), content_type: 'application/json'
boletos = JSON.parse(boletos.body)
```

```python
import requests

# ...
# É necessário ser do tipo list
boletos = [{
  'cliente': "00000000000",
  'desricao': "Boleto 1",
  'linha_digitavel': '00000000000000000000000000000000000000',
},{
  'cliente': "00000000001",
  'desricao': "Boleto 2",
  'linha_digitavel': '00000000000000000000000000000000000001',
}
# ...
]

req.post('{}/empresa/registrar_boletos/', json=boletos)

```

```shell
curl "https://newinfotech.com.br/api/empresa/registrar_boletos/"
  -H "Authorization: <Seu token aqui>"
  -H "Content-Type: application/json"
  -X POST -d '[{"cliente": "00000000000", "descricao': "Boleto 1", "linha_digitavel": "000000000000000000000000000000"}]'
```


> O comando acima retornará o seguinte JSON:

```json
{
  "status": "1 resgistros salvo(s) com sucesso", 
  "cont": 1
}
```

Use este endpoint para enviar uma lista de Boletos (Array) para o nosso sistema

<aside class="notice">
Observe se a contagem de itens na resposta corresponde à quantidade de itens enviados, caso não corresponda, pode ser que exista erro em algum item enviado
</aside>

### Requisição HTTP

`POST https://newinfotech.com.br/api/empresa/registrar_boletos/`

### Parâmetros

Parameter | Description
--------- | -----------
lista_de_boletos | Array com informações dos boletos a serem adicionados ao sistema

> Os dados necessários para o cadastro do boleto estão listados no JSON abaixo:

```json
{
  "cliente": "<cpf_cnpj_do_cliente>",
  "descricao": "<descricao_da_cobrança>",
  "linha_digitavel": "<linha_digitavel>"
}
```

# Promissórias

## Obtendo todas as promissórias

```ruby
require 'rest-client'
require 'json'

# ...
promissorias = api['promissorias/'].get
promissorias = JSON.parse(promissorias.body)
```

```python
import requests

# ...
req.get('{}/promissorias'.format(root))
```

```shell
curl "https://newinfotech.com.br/api/promissorias"
  -H "Authorization: <Seu token aqui>"
```


> O comando acima retornará o seguinte JSON:

```json
[
    {
        "id": 27575,
        "cliente": "16023", # "CPF/CNPJ ou outro identificador usado"
        "descricao": "Descrição da cobrança",
        "valor": 100.0,
        "data_vencimento": "2017-10-30",
        "pago": false,
        "create_datetime": "2017-10-02T20:24:45.747269Z",
        "write_datetime": "2017-10-02T20:24:45.747300Z",
        "valor_por_extenso": "cem reais",
        "nome_credor": "NOME DA SUA EMPRESA",
        "cpf_cnpj_credor": "CNPJ DA SUA EMPRESA",
        "pagavel_em": "opcional",
        "local_emissao": "opcional",
        "nome_devedor": "NOME DO CLIENTE",
        "cpf_cnpj_devedor": "CPF/CNPJ DO CLIENTE",
        "endereco_devedor": "opcional",
        "despesa": null,
        "categoria": null,
        "parceiro": "SEU ID"
    },
    ...
]

```

Este endpoint retorna todos as promissórias cadastradas pela empresa.

### Requisição HTTP

`GET https://newinfotech.com.br/api/promissorias`

### Parâmetros

<aside class="notice">
Este endpoint não aceita parâmetros adicionais
</aside>

## Obtendo uma promissória específica

```ruby
require 'rest-client'
require 'json'

# ...
promissoria = api['promissorias/<id>'].get
promissoria = JSON.parse promissoria.body
```

```python
import requests

# ...
promissoria = req.get('{}/promissorias/<id>')
promissoria = promissoria.content
```

```shell
curl "https://newinfotech.com.br/api/promissorias/<id>"
  -H "Authorization: <seu_token_aqui>"
```


> O comando acima retornará o seguinte JSON:

```json
{
    "id": 27575,
    "cliente": "16023", # "CPF/CNPJ ou outro identificador usado"
    "descricao": "Descrição da cobrança",
    "valor": 100.0,
    "data_vencimento": "2017-10-30",
    "pago": false,
    "create_datetime": "2017-10-02T20:24:45.747269Z",
    "write_datetime": "2017-10-02T20:24:45.747300Z",
    "valor_por_extenso": "cem reais",
    "nome_credor": "NOME DA SUA EMPRESA",
    "cpf_cnpj_credor": "CNPJ DA SUA EMPRESA",
    "pagavel_em": "opcional",
    "local_emissao": "opcional",
    "nome_devedor": "NOME DO CLIENTE",
    "cpf_cnpj_devedor": "CPF/CNPJ DO CLIENTE",
    "endereco_devedor": "opcional",
    "despesa": null,
    "categoria": null,
    "parceiro": "SEU ID"
},
```

Este endpoint retorna uma promissória específica

> Subistitua `<id>` pelo ID da promissória que deseja obter

### Requisição HTTP

`GET https://newinfotech.com.br/api/promissorias/<id>`

### URL Parameters

Parameter | Description
--------- | -----------
id | O `id` da promissória que se deseja obter


## Enviando uma lista de promissorias

```ruby
require 'rest-client'
require 'json'

# ...
# É necessário ser do tipo Array
promissorias = [{
  cpf_cnpj_devedor: "00000000000",
  desricao: "Boleto 1",
  valor: '100',
  data_vencimento: "2017-10-30"
},{
  cpf_cnpj_devedor: "00000000001",
  desricao: "Boleto 2",
  valor: '100',
  data_vencimento: "2017-10-30"
}
# ...
]
promissorias = api['empresa/registrar_promissorias/'].post JSON.generate(promissorias), content_type: 'application/json'
promissorias = JSON.parse(promissorias.body)
```

```python
import requests

# ...
# É necessário ser do tipo list
promissorias = [{
  'cpf_cnpj_devedor': "00000000000",
  'desricao': "Boleto 1",
  'valor': '100',
  'data_vencimento': "2017-10-30"
},{
  'cpf_cnpj_devedor': "00000000001",
  'desricao': "Boleto 2",
  'valor': '100',
  'data_vencimento': "2017-10-30"
}
# ...
]

req.post('{}/empresa/registrar_promissorias/', json=promissorias)

```

```shell
curl "https://newinfotech.com.br/api/empresa/registrar_promissorias/"
  -H "Authorization: <Seu token aqui>"
  -H "Content-Type: application/json"
  -X POST -d '[{"cpf_cnpj_devedor": "00000000000", "descricao': "Promissória 1", "valor": "100", "data_vencimento": "2017-10-30"}]'
```


> O comando acima retornará o seguinte JSON:

```json
{
  "status": "1 resgistros salvo(s) com sucesso", 
  "cont": 1
}
```

Use este endpoint para enviar uma lista de Promissórias (Array) para o nosso sistema

<aside class="notice">
Observe se a contagem de itens na resposta corresponde à quantidade de itens enviados, caso não corresponda, pode ser que exista erro em algum item enviado, você também pode tentar enviar os itens individualmente pelo endpoint `POST https://newinfotech.com.br/api/promissorias/`
</aside>

### Requisição HTTP

`POST https://newinfotech.com.br/api/empresa/registrar_promissorias/`

### Parâmetros

Parameter | Description
--------- | -----------
lista_de_promissorias | Array com informações das promissórias a serem adicionados ao sistema

> Os dados necessários para o cadastro da promissória estão listados no JSON abaixo:

```json
{
  "cpf_cnpj_devedor": "<cpf_cnpj_do_cliente>",
  "descricao": "<descricao_da_cobrança>",
  "Valor": "<linha_digitavel>",
  "data_vencimento": "<data no formato ISO>"
}
```