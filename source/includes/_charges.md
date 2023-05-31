# Cobranças

## Gerando uma nova cobrança

```ruby
require "uri"
require "json"
require "net/http"

url = URI("http://homolog.youpay.digital/api/charge/new")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Content-Type"] = "application/json"
request["idEstablishment"] = "<seu_establishment_id>"
request["Accept"] = "application/json"
request["Authorization"] = "Bearer <token_exemplo>"
request.body = JSON.dump({
  "description": "Pagamento de 10 coxinhas de frango",
  "obs": "Esta é uma cobrança exemplo da API",
  "type_transaction_installments": "FULL",
  "installments_max_allow": 1,
  "amount": 10.58,
  "due_at": "2023-09-30 02:15:25",
  "allow_card": true,
  "allow_pix": true,
  "allow_boleto": true,
  "use_only_once": true,
  "split": [
    {
      "id_establishment": "<establishment_id_exemplo>",
      "amount": 2,
      "type": "FIXED"
    }
  ],
  "advanced": [
    {
      "interest": {
        "value": "0.00"
      }
    },
    {
      "fine": {
        "value": "0.00"
      }
    },
    {
      "discount": {
        "value": "0.0",
        "dueDateLimitDays": 0,
        "type": "FIXED"
      }
    }
  ]
})

response = http.request(request)
puts response.read_body
```

```python
import requests
import json

url = "http://homolog.youpay.digital/api/charge/new"

payload = json.dumps({
  "description": "Pagamento de 10 coxinhas de frango",
  "obs": "Esta é uma cobrança exemplo da API",
  "type_transaction_installments": "FULL",
  "installments_max_allow": 1,
  "amount": 10.58,
  "due_at": "2023-09-30 02:15:25",
  "allow_card": True,
  "allow_pix": True,
  "allow_boleto": True,
  "use_only_once": True,
  "split": [
    {
      "id_establishment": "<establishment_id_exemplo>",
      "amount": 2,
      "type": "FIXED"
    }
  ],
  "advanced": [
    {
      "interest": {
        "value": "0.00"
      }
    },
    {
      "fine": {
        "value": "0.00"
      }
    },
    {
      "discount": {
        "value": "0.0",
        "dueDateLimitDays": 0,
        "type": "FIXED"
      }
    }
  ]
})
headers = {
  'Content-Type': 'application/json',
  'idEstablishment': '<seu_establishment_id>',
  'Accept': 'application/json',
  'Authorization': 'Bearer <token_exemplo>'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```

```shell
curl --location --request POST 'http://homolog.youpay.digital/api/charge/new' \
--header 'Content-Type: application/json' \
--header 'idEstablishment: <seu_establishment_id>' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer <token_exemplo>' \
--data '{
    "description": "Pagamento de 10 coxinhas de frango",
    "obs": "Esta é uma cobrança exemplo da API",
    "type_transaction_installments": "FULL",
    "installments_max_allow": 1,
    "amount": 10.58,
    "due_at": "2023-09-30 02:15:25",
    "allow_card": true,
    "allow_pix": true,
    "allow_boleto": true,
    "use_only_once": true,
    "split": [
        {
            "id_establishment": "<establishment_id_exemplo>",
            "amount": 2,
            "type": "FIXED"
        }
    ],
    "advanced": [
        {
            "interest": {
                "value": "0.00"
            }
        },
        {
            "fine": {
                "value": "0.00"
            }
        },
        {
            "discount": {
                "value": "0.0",
                "dueDateLimitDays": 0,
                "type": "FIXED"
            }
        }
    ]
}'
```

```javascript
const myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json");
myHeaders.append("idEstablishment", "<seu_establishment_id>");
myHeaders.append("Accept", "application/json");
myHeaders.append("Authorization", "Bearer <token_exemplo>");

const raw = JSON.stringify({
  description: "Pagamento de 10 coxinhas de frango",
  obs: "Esta é uma cobrança exemplo da API",
  type_transaction_installments: "FULL",
  installments_max_allow: 1,
  amount: 10.58,
  due_at: "2023-09-30 02:15:25",
  allow_card: true,
  allow_pix: true,
  allow_boleto: true,
  use_only_once: true,
  split: [
    {
      id_establishment: "<establishment_id_exemplo>",
      amount: 2,
      type: "FIXED",
    },
  ],
  advanced: [
    {
      interest: {
        value: "0.00",
      },
    },
    {
      fine: {
        value: "0.00",
      },
    },
    {
      discount: {
        value: "0.0",
        dueDateLimitDays: 0,
        type: "FIXED",
      },
    },
  ],
});

const requestOptions = {
  method: "POST",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("http://homolog.youpay.digital/api/charge/new", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\n    \"description\": \"Pagamento de 10 coxinhas de frango\",\n    \"obs\": \"Esta é uma cobrança exemplo da API\",\n    \"type_transaction_installments\": \"FULL\",\n    \"installments_max_allow\": 1,\n    \"amount\": 10.58,\n    \"due_at\": \"2023-09-30 02:15:25\",\n    \"allow_card\": true,\n    \"allow_pix\": true,\n    \"allow_boleto\": true,\n    \"use_only_once\": true,\n    \"split\": [\n        {\n            \"id_establishment\": \"<establishment_id_exemplo>\",\n            \"amount\": 2,\n            \"type\": \"FIXED\"\n        }\n    ],\n    \"advanced\": [\n        {\n            \"interest\": {\n                \"value\": \"0.00\"\n            }\n        },\n        {\n            \"fine\": {\n                \"value\": \"0.00\"\n            }\n        },\n        {\n            \"discount\": {\n                \"value\": \"0.0\",\n                \"dueDateLimitDays\": 0,\n                \"type\": \"FIXED\"\n            }\n        }\n    ]\n}");
Request request = new Request.Builder()
  .url("http://homolog.youpay.digital/api/charge/new")
  .method("POST", body)
  .addHeader("Content-Type", "application/json")
  .addHeader("idEstablishment", "<seu_establishment_id>")
  .addHeader("Accept", "application/json")
  .addHeader("Authorization", "Bearer <token_exemplo>")
  .build();
Response response = client.newCall(request).execute();
```

> Se certifique de trocar token_exemplo, seu_establishment_id e establishment_id_exemplo pelos dados corretos.
> A requisição acima retorna um JSON estruturado desta forma:

```json
{
  "id": "a10001b7-a1b6-4783-bc56-1b54cc630780",
  "description": "Pagamento de 10 coxinhas de frango",
  "obs": "Esta é uma cobrança exemplo da API",
  "id_establishment": "<seu_establishment_id>",
  "type_transaction_installments": "FULL",
  "amount": 10.58,
  "due_at": "2023-09-30T05:15:25.000000Z",
  "method_card_allow": true,
  "method_pix_allow": true,
  "method_boleto_allow": true,
  "use_only_once": 1,
  "installments_max_allow": 1,
  "id_user_created_charge": null,
  "type_transaction": null,
  "name_notification": null,
  "cellphone_notification": null,
  "email_notification": null,
  "discounts": "[{\"interest\":{\"value\":\"0.00\"}},{\"fine\":{\"value\":\"0.00\"}},{\"discount\":{\"value\":\"0.0\",\"dueDateLimitDays\":0,\"type\":\"FIXED\"}}]",
  "split": [
    {
      "id_establishment": "<establishment_id_exemplo>",
      "amount": 2,
      "type": "FIXED"
    }
  ],
  "updated_at": "2023-05-31T11:52:07.000000Z",
  "created_at": "2023-05-31T11:52:07.000000Z"
}
```

Para gerar uma nova cobrança por meio da API da Youpay é necessário realizar um **`POST`** para **`http://homolog.youpay.digital/api/charge/new`** passando os seguintes parâmetros:

| Parâmetro                                            | Descrição                                                 | Tipo      |
| ---------------------------------------------------- | --------------------------------------------------------- | --------- |
| description <sub>Obrigatório</sub>                   | Descrição/Título da cobrança                              | String    |
| obs                                                  | Campo para observações extras da cobrança                 | string    |
| type_transaction_installments <sub>Obrigatório</sub> | Tipo de parcelamento da cobrança                          | string    |
| installments_max_allow <sub>Obrigatório</sub>        | Número máximo permitido de parcelas                       | string    |
| amount <sub>Obrigatório</sub>                        | Valor da cobrança                                         | Float     |
| due_at <sub>Obrigatório</sub>                        | Data de vencimento da cobrança                            | Timestamp |
| allow_card <sub>Obrigatório</sub>                    | Flag para permitir pagamento com cartão                   | Boolean   |
| allow_pix <sub>Obrigatório</sub>                     | Flag para permitir pagamento via Pix                      | Boolean   |
| allow_boleto <sub>Obrigatório</sub>                  | Flag para permitir pagamento com boleto                   | Boolean   |
| use_only_once <sub>Obrigatório</sub>                 | Flag para permitir o pagamento da cobrança apenas uma vez | Boolean   |
| id_user_created_charge                               | Identificador do usuário que criou a cobrança             | String    |
| name_notification                                    | Nome para uma notificação via telefone ou e-mail          | String    |
| cellphone_notification                               | Telefone que irá receber a notificação                    | String    |
| email_notification                                   | E-mail que irá receber a notificação                      | String    |

### Split de pagamento

Com a API da Youpay é possível configurar o split do pagamento na hora da criação da cobrança.

Para isso, é necessário passar no corpo da requisição um `Array` chamado **`split`** composto por objetos seguindo o padrão abaixo:

| Parâmetro                               | Descrição                                                        | Tipo   |
| --------------------------------------- | ---------------------------------------------------------------- | ------ |
| id_establishment <sub>Obrigatório</sub> | Identificador do establishment resonsável por dividir a cobrança | String |
| amount <sub>Obrigatório</sub>           | Valor fixo ou percentual do split                                | Float  |
| type <sub>Obrigatório</sub>             | Tipo do split                                                    | String |

Um split de pagamentos pode ser do tipo `FIXED`, em que o campo `amount` é tratado como um valor em `R$`. Ou do tipo `PERCENTAGE`, em que o campo `amount` é tratado como um percentual do valor original da cobrança.

### Juros, multas e descontos

Para o cálculo de juros, multas e descontos nas cobranças é necessário passar no corpo da requisição um `Array` chamado **`advanced`** composto pelos objetos `interest`, `fine` e `discount` seguindo o padrão abaixo:

#### Juros e multas

| Parâmetro                    | Descrição                             | Tipo   |
| ---------------------------- | ------------------------------------- | ------ |
| value <sub>Obrigatório</sub> | Valor (em `R$`) dos juros ou da multa | Float  |
| type                         | Tipo do valor dos juros ou multa      | String |

#### Descontos

| Parâmetro                    | Descrição                                                                  | Tipo   |
| ---------------------------- | -------------------------------------------------------------------------- | ------ |
| value <sub>Obrigatório</sub> | Valor do desconto                                                          | Float  |
| dueDateLimitDays             | Número de dias que o desconto continua valendo antes da data de vencimento | Int    |
| type                         | Tipo do valor do desconto                                                  | String |

<aside class="notice">
Assim como no split de pagamentos, o campo `type` pode ser do tipo `FIXED` ou do tipo `PERCENTAGE`, seguindo as mesmas regras já mencionadas.
</aside>

### Possíveis erros

> idEstablishment não informado no cabeçalho da requisição

```json
{
  "msg": "Não permitido!.",
  "details": "Você precisa informar o idEstablishment no header."
}
```

> O client_id utilizado para criar o token não está vinculado a um establishment, ou não tem permissões para gerar uma cobrança

```json
{
  "msg": "Não permitido!.",
  "details": "O ID Client OAuth não está vinculado a nenhum estabelecimento, ou não tem permissão para o mesmo."
}
```

> Algum campo obrigatório não foi informado

```json
{
  "message": "The given data was invalid.",
  "errors": {
    "<nome_do_campo>": ["O campo <nome_do_campo> é obrigatório."]
  }
}
```

> O campo due_date é menor do que o dia atual

```json
{
  "msg": "A cobrança não pode ser criada!",
  "details": "A data de vencimento precisa ser igual ou maior que hoje."
}
```

> Campo id_establishment no array de split não é um identificador válido

```json
{
  "msg": "A cobrança não pode ser criada!",
  "details": "O ID do estabelecimento <identificador_inválido> não é válido."
}
```

> Campo id_establishment no array de split é igual ao idEstablishment do cabeçalho da requisição

```json
{
  "msg": "A cobrança não pode ser criada!",
  "details": "Um dos estabelecimentos contidos na regra do split é o mesmo do dono da cobrança."
}
```

> Campo id_establishment no array de split não foi fornecido

```json
{
  "msg": "A cobrança não pode ser criada!",
  "details": "O split deve ser um array de objetos."
}
```

> O array de split não possui objetos

```json
{
  "msg": "A cobrança não pode ser criada!",
  "details": "O split deve ser um array de objetos."
}
```

Caso algum campo não seja preenchido corretamente, você pode se deparar com algum erro na hora de realizar a requisição.

Ao lado estão alguns errors comuns e suas causas.

De maneira geral, os erros de criação de cobranças seguem sempre o seguinte padrão:

| Campo   | Descrição                           | Tipo   |
| ------- | ----------------------------------- | ------ |
| msg     | Uma mensagem sobre o erro           | String |
| details | Mais detalhes sobre a causa do erro | String |

Além desse padrão de respostas, os [status HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) utilzados nos casos de erro também visam ajudá-lo a entender o que pode ter ocorrido, abaixo está uma lista de status utilizados nesse fluxo e o que podem significar:

| Código | Nome                  | Descrição                                                                                               |
| ------ | --------------------- | ------------------------------------------------------------------------------------------------------- |
| 400    | Bad Request           | Alguma informação na requisição não segue o padrão desejado, olhe a mensagem de erro para mais detalhes |
| 403    | Forbidden             | O usuário não possui os direitos para acessar o conteúdo                                                |
| 422    | Unprocessable Content | Alguma informação obrigatória não foi fornecida no corpo da requisição                                  |

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
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require("kittn");

let api = kittn.authorize("meowmeowmeow");
let max = api.kittens.get(2);
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

| Parameter | Description                      |
| --------- | -------------------------------- |
| ID        | The ID of the kitten to retrieve |

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require("kittn");

let api = kittn.authorize("meowmeowmeow");
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted": ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the kitten to delete |
