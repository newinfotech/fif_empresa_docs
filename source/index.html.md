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

# Autenticação

> Use o seguinte código para autorizar o acesso a nossa API:

```ruby
require 'rest-client'

token = "<Seu token obtido na interface de empresa>"
dados = RestClient.get "endpoint_de_sua_escolha", content_type: :json, Authorization: token 
```

```python
import requests

req = requests.Session()
req.headers['Authorization'] = "<Seu token obtido na interface de empresa>"
```

```shell
# Em shell, só é necessário passar o cabeçalho correto
curl "endpoint_de_sua_escolha"
  -H "Authorization: <Seu token obtido na interface de empresa>"
```

> Não esqueça de subistituir `<Seu token obtido na interface de empresa>` com o Token obtido na página de [Configurações](https://newinfotech.com.br/empresas/#/config/integracao).

> Subistitua `endpoint_de_sua_escolha` por algum dos endpoints desta documentação.

Nossa API usa Tokens para Autenticação e Autorização do usuário, para obter um token de acesso, visite suas [Configurações](https://newinfotech.com.br/empresas/#/config/integracao).

Para qualquer requisição autenticada a nossa API, o desenvolvedor deve usar o cabeçalho `Authorization` como abaixo:

`Authorization: Token c34no3y57y8n75y845t7vywbo7858tv7vmw8`

<aside class="notice">
Subistitua <code>Token c34no3y57y8n75y845t7vywbo7858tv7vmw8</code> pelo seu Token.
</aside>

# Clientes

## Obter todos os clientes

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```


> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

Este endpoint retorna todos os clientes vinculados a empresa.

### Requisição HTTP

`GET https://newinfotech.com.br/api/clientes`

### Parâmetros


<aside class="notice">
Este endpoint não aceita parâmetros
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```


> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

