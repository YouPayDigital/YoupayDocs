# Cartões

## Tokenização do cartão

```ruby
require "uri"
require "json"
require "net/http"

url = URI("http://homolog.youpay.digital/api/charge/cards/add")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Accept"] = "application/json"
request["idEstablishment"] = "<seu_establishment_id>"
request["Content-Type"] = "application/json"
request["Authorization"] = "Bearer <token_exemplo>
request.body = JSON.dump({
  "description": "Cartão da Middle-Earth",
  "cardholder_name": "Sauron",
  "cpf": "11834644445",
  "id_account": 1,
  "card_number": "4012001037141112",
  "brand": "Visa",
  "expiration_info": "06/25",
  "cvc": "132",
  "is_default": true
})

response = http.request(request)
puts response.read_body
```

```python
import requests
import json

url = "http://homolog.youpay.digital/api/charge/cards/add"

payload = json.dumps({
  "description": "Cartão da Middle-Earth",
  "cardholder_name": "Sauron",
  "cpf": "11834644445",
  "id_account": 1,
  "card_number": "4012001037141112",
  "brand": "Visa",
  "expiration_info": "06/25",
  "cvc": "132",
  "is_default": True
})
headers = {
  'Accept': 'application/json',
  'idEstablishment': '<seu_establishment_id>',
  'Content-Type': 'application/json',
  'Authorization': 'Bearer <token_exemplo>'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'http://homolog.youpay.digital/api/charge/cards/add' \
--header 'Accept: application/json' \
--header 'idEstablishment: <seu_establishment_id>' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <token_exemplo>' \
--data '{
  "description": "Cartão da Middle-Earth",
  "cardholder_name": "Sauron",
  "cpf": "11834644445",
  "id_account": 1,
  "card_number": "4012001037141112",
  "brand": "Visa",
  "expiration_info": "06/25",
  "cvc": "132",
  "is_default": true
}'
```

```javascript
const myHeaders = new Headers();
myHeaders.append("Accept", "application/json");
myHeaders.append("idEstablishment", "<seu_establishment_id>");
myHeaders.append("Content-Type", "application/json");
myHeaders.append("Authorization", "Bearer <token_exemplo>");

const raw = JSON.stringify({
  description: "Cartão da Middle-Earth",
  cardholder_name: "Sauron",
  cpf: "11834644445",
  id_account: 1,
  card_number: "4012001037141112",
  brand: "Visa",
  expiration_info: "06/25",
  cvc: "132",
  is_default: true,
});

const requestOptions = {
  method: "POST",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("http://homolog.youpay.digital/api/charge/cards/add", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\n  \"description\": \"Cartão da Middle-Earth\",\n  \"cardholder_name\": \"Sauron\",\n  \"cpf\": \"11834644445\",\n  \"id_account\": 1,\n  \"card_number\": \"4012001037141112\",\n  \"brand\": \"Visa\",\n  \"expiration_info\": \"06/25\",\n  \"cvc\": \"132\",\n  \"is_default\": true\n}");
Request request = new Request.Builder()
  .url("http://homolog.youpay.digital/api/charge/cards/add")
  .method("POST", body)
  .addHeader("Accept", "application/json")
  .addHeader("idEstablishment", "<seu_establishment_id>")
  .addHeader("Content-Type", "application/json")
  .addHeader("Authorization", "Bearer <token_exemplo>")
  .build();
Response response = client.newCall(request).execute();
```

> Se certifique de trocar token_exemplo e seu_establishment_id pelos dados corretos.
> A requisição acima retorna um JSON estruturado desta forma:

```json
{
  "msg": "Cartão cadastrado com sucesso...",
  "details": {
    "number": "**** **** **** 1112",
    "description": "Cartão da Middle-Earth",
    "id_card_type": 3,
    "id_account": null,
    "is_default": true,
    "enabled": 1,
    "enabled_internal": 1,
    "allow_alter_limit": 1,
    "daily_limit": 0,
    "limit": 0,
    "limit_internal": 0,
    "due_date": null,
    "card_id": "d2296faf-8f2f-4b6b-92f0-72479ce6b2ab",
    "cvc": "132",
    "brand": "Visa",
    "expiration_info": "06/25",
    "updated_at": "2023-05-31T19:41:14.000000Z",
    "created_at": "2023-05-31T19:41:14.000000Z",
    "id": 323
  }
}
```

A fim de tornar seus pagamentos ainda mais seguros, é possível tokenizar um cartão e utilizar apenas o token gerado em transações futuras. Sem a necessidade de enviar todos os dados do cartão em todas as requisições.

### Requisição HTTP

`POST http://homolog.youpay.digital/api/charge/cards/add`

### Corpo da requisição

| Parâmetro                              | Descrição                                                | Tipo    |
| -------------------------------------- | -------------------------------------------------------- | ------- |
| cpf <sub>Obrigatório</sub>             | CPF do titular do cartão                                 | String  |
| brand <sub>Obrigatório</sub>           | Bandeira do cartão                                       | String  |
| card_number <sub>Obrigatório</sub>     | Número do cartão                                         | Int     |
| expiration_info <sub>Obrigatório</sub> | Data de validade do cartão no formato MM/AA              | String  |
| description <sub>Obrigatório</sub>     | Descrição do cartão                                      | String  |
| cardholder_name <sub>Obrigatório</sub> | Nome do portador do cartão                               | String  |
| cvc <sub>Obrigatório</sub>             | Código verificador do cartão                             | String  |
| is_default                             | Será o cartão utilizado por padrão em pagamentos futuros | Boolean |

<aside class="notice">
É importante notar que o número do cartão é censurado na resposta, a fim de garantir o máximo de sigilo.
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

> Um erro não mapeado aconteceu

```json
{
  "message": "Não foi possível adicionar o cartão",
  "name": "Erro genérico",
  "status_code": 409,
  "details": "<detalhes_do_erro>"
}
```

Caso algum campo não seja preenchido corretamente, você pode se deparar com algum erro na hora de realizar a requisição.

Ao lado estão alguns errors comuns e suas causas.

De maneira geral, caso todos os dados sejam passados corretamente na requisição, os erros de tokenização do cartão são bastante raros, sendo necessário conferir os detalhes desses casos isolados.

Abaixo está uma lista de status utilizados nesse fluxo e o que podem significar:

| Código | Nome                  | Descrição                                                                |
| ------ | --------------------- | ------------------------------------------------------------------------ |
| 409    | Conflict              | Há algum conflito entre o estado esperado e o estado atual da requisição |
| 422    | Unprocessable Content | Alguma informação obrigatória não foi fornecida no corpo da requisição   |
