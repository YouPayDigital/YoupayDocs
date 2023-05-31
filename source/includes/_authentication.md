# Autenticação

A API de cobranças da Youpay utiliza a especificação [OAuth2](https://oauth.net/2/) para lidar com autenticação.

Para realizar qualquer outra requisição, será necessário se autenticar por meio de um token.

## Gerando um token

> Exemplo de autenticação:

```ruby
require "uri"
require "json"
require "net/http"

url = URI("https://homolog.youpay.digital/oauth/token")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Accept"] = "application/json"
request["Content-Type"] = "application/json"
request.body = JSON.dump({
  "grant_type": "client_credentials",
  "client_id": "id_exemplo",
  "client_secret": "secret_exemplo",
  "scope": "charges"
})

response = http.request(request)
puts response.read_body

```

```python
import requests
import json

url = "https://homolog.youpay.digital/oauth/token"

payload = json.dumps({
  "grant_type": "client_credentials",
  "client_id": "id_exemplo",
  "client_secret": "secret_exemplo",
  "scope": "charges"
})
headers = {
  'Accept': 'application/json',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```

```shell
curl --location --request POST 'https://homolog.youpay.digital/oauth/token' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data '{
    "grant_type": "client_credentials",
    "client_id": "id_exemplo",
    "client_secret": "secret_exemplo",
    "scope": "charges"
}'
```

```javascript
const myHeaders = new Headers();
myHeaders.append("Accept", "application/json");
myHeaders.append("Content-Type", "application/json");

const raw = JSON.stringify({
  grant_type: "client_credentials",
  client_id: "id_exemplo",
  client_secret: "secret_exemplo",
  scope: "charges",
});

const requestOptions = {
  method: "POST",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://homolog.youpay.digital/oauth/token", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();

MediaType mediaType = MediaType.parse("application/json");

RequestBody body = RequestBody.create(mediaType, "{\n    \"grant_type\": \"client_credentials\",\n    \"client_id\": \"id_exemplo\",\n    \"client_secret\": \"secret_exemplo\",\n    \"scope\": \"charges\"\n}");

Request request = new Request.Builder()
  .url("https://homolog.youpay.digital/oauth/token")
  .method("POST", body)
  .addHeader("Accept", "application/json")
  .addHeader("Content-Type", "application/json")
  .build();

Response response = client.newCall(request).execute();
```

> Se certifique de trocar `id_exemplo` e `secret_exemplo` pelas suas credenciais.

> A requisição acima retorna um JSON estruturado desta forma:

```json
{
  "token_type": "Bearer",
  "expires_in": 31622400,
  "access_token": "<token_exemplo>"
}
```

Para gerá-lo é necessário realizar um **`POST`** para **`https://homolog.youpay.digital/oauth/token`**, passando as seguintes informações:

| Parâmetro                              | Descrição                                                                 | Tipo   |
| -------------------------------------- | ------------------------------------------------------------------------- | ------ |
| grant_type _<sub>Obrigatório</sub>_    | Um tipo de [grant type do OAuth2](https://oauth.net/2/grant-types/)       | String |
| client_id _<sub>Obrigatório</sub>_     | O identificador da sua conta na nossa base                                | String |
| client_secret _<sub>Obrigatório</sub>_ | O secret da sua conta na nossa base                                       | String |
| scope _<sub>Obrigatório</sub>_         | O [escopo de acesso](https://oauth.net/2/scope/) que o token irá garantir | String |

Caso a requisição ocorra como o esperado, você receberá uma resposta no seguinte padrão:

| Campo        | Descrição                                      | Tipo   |
| ------------ | ---------------------------------------------- | ------ |
| token_type   | O tipo do token emitido, por exemplo: `Bearer` | String |
| expires_in   | O tempo, em segundos, de validade do token     | Int    |
| access_token | O token de autenticação                        | String |

## Possíveis erros

> Campo grant_type não foi fornecido

```json
{
  "error": "unsupported_grant_type",
  "error_description": "The authorization grant type is not supported by the authorization server.",
  "hint": "Check that all required parameters have been provided",
  "message": "The authorization grant type is not supported by the authorization server."
}
```

> Campo client_id não foi fornecido

```json
{
  "error": "invalid_request",
  "error_description": "The request is missing a required parameter, includes an invalid parameter value, includes a parameter more than once, or is otherwise malformed.",
  "hint": "Check the `client_id` parameter",
  "message": "The request is missing a required parameter, includes an invalid parameter value, includes a parameter more than once, or is otherwise malformed."
}
```

> Campo client_secret não foi fornecido

```json
{
  "error": "invalid_client",
  "error_description": "Client authentication failed",
  "message": "Client authentication failed"
}
```

Caso algum campo não seja preenchido corretamente, você pode se deparar com algum erro na hora de realizar a requisição.

Ao lado estão alguns errors comuns e suas causas.

De maneira geral, os erros de autenticação seguem sempre o seguinte padrão:

| Campo             | Descrição                                                    | Tipo   |
| ----------------- | ------------------------------------------------------------ | ------ |
| error             | O tipo do erro, por exemplo: `invalid_client`                | String |
| error_description | A descrição do erro, com mais detalhes sobre o que aconteceu | String |
| message           | A mensagem gerada pela API                                   | String |

Em alguns outros casos, como quando o `client_id` não é fornecido, há ainda um outro campo:

| Campo | Descrição                                      | Tipo   |
| ----- | ---------------------------------------------- | ------ |
| hint  | Uma dica da API sobre qual pode ser o problema | String |
