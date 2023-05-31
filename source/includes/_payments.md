# Pagamentos

## Realizando um pagamento

```ruby
require "uri"
require "json"
require "net/http"

url = URI("http://homolog.youpay.digital/api/charge/payment")

http = Net::HTTP.new(url.host, url.port);
request = Net::HTTP::Post.new(url)
request["Content-Type"] = "application/json"
request["idEstablishment"] = "<seu_establishment_id>"
request["Accept"] = "application/json"
request["Authorization"] = "Bearer <token_exemplo>"
request.body = JSON.dump({
  "method": "bank_slip",
  "description": "Pagamento  - novo anel",
  "amount": 55.55,
  "idCharge": "744cee94-308f-41cb-b05f-956ce016d456",
  "customerName": "Frodo Bolseiro",
  "customerTypeDocument": "CPF",
  "customerDocument": "69441700436",
  "customerStreet": "Rua dos Bolseiros",
  "customerNumber": "9",
  "customerDistrict": "Condadinho",
  "customerCity": "Condado",
  "customerCellphone": nil,
  "customerEmail": "frodo.bolseiro@sociedade-do-anel.com",
  "customerState": "Middle-Earth",
  "customerPostalCode": "9000000"
})

response = http.request(request)
puts response.read_body
```

```python
import requests
import json

url = "http://homolog.youpay.digital/api/charge/payment"

payload = json.dumps({
  "method": "bank_slip",
  "description": "Pagamento  - novo anel",
  "amount": 55.55,
  "idCharge": "744cee94-308f-41cb-b05f-956ce016d456",
  "customerName": "Frodo Bolseiro",
  "customerTypeDocument": "CPF",
  "customerDocument": "69441700436",
  "customerStreet": "Rua dos Bolseiros",
  "customerNumber": "9",
  "customerDistrict": "Condadinho",
  "customerCity": "Condado",
  "customerCellphone": None,
  "customerEmail": "frodo.bolseiro@sociedade-do-anel.com",
  "customerState": "Middle-Earth",
  "customerPostalCode": "9000000"
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
curl --location --request POST 'http://homolog.youpay.digital/api/charge/payment' \
--header 'Content-Type: application/json' \
--header 'idEstablishment: cad21c87-aca9-409d-84d1-ac0ddb983b88' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer <token_exemplo>' \
--data-raw '{
  "method": "bank_slip",
  "description": "Pagamento  - novo anel",
  "amount": 55.55,
  "idCharge": "<seu_establishment_id>",
  "customerName": "Frodo Bolseiro",
  "customerTypeDocument": "CPF",
  "customerDocument": "69441700436",
  "customerStreet": "Rua dos Bolseiros",
  "customerNumber": "9",
  "customerDistrict": "Condadinho",
  "customerCity": "Condado",
  "customerCellphone": null,
  "customerEmail": "frodo.bolseiro@sociedade-do-anel.com",
  "customerState": "Middle-Earth",
  "customerPostalCode": "9000000"
}'
```

```javascript
const myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json");
myHeaders.append("idEstablishment", "cad21c87-aca9-409d-84d1-ac0ddb983b88");
myHeaders.append("Accept", "application/json");
myHeaders.append("Authorization", "Bearer <token_exemplo>");

const raw = JSON.stringify({
  method: "bank_slip",
  description: "Pagamento  - novo anel",
  amount: 55.55,
  idCharge: "<seu_establishment_id>",
  customerName: "Frodo Bolseiro",
  customerTypeDocument: "CPF",
  customerDocument: "69441700436",
  customerStreet: "Rua dos Bolseiros",
  customerNumber: "9",
  customerDistrict: "Condadinho",
  customerCity: "Condado",
  customerCellphone: null,
  customerEmail: "frodo.bolseiro@sociedade-do-anel.com",
  customerState: "Middle-Earth",
  customerPostalCode: "9000000",
});

const requestOptions = {
  method: "POST",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("http://homolog.youpay.digital/api/charge/payment", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\n  \"method\": \"bank_slip\",\n  \"description\": \"Pagamento  - novo anel\",\n  \"amount\": 55.55,\n  \"idCharge\": \"744cee94-308f-41cb-b05f-956ce016d456\",\n  \"customerName\": \"Frodo Bolseiro\",\n  \"customerTypeDocument\": \"CPF\",\n  \"customerDocument\": \"69441700436\",\n  \"customerStreet\": \"Rua dos Bolseiros\",\n  \"customerNumber\": \"9\",\n  \"customerDistrict\": \"Condadinho\",\n  \"customerCity\": \"Condado\",\n  \"customerCellphone\": null,\n  \"customerEmail\": \"frodo.bolseiro@sociedade-do-anel.com\",\n  \"customerState\": \"Middle-Earth\",\n  \"customerPostalCode\": \"9000000\"\n}");
Request request = new Request.Builder()
  .url("http://homolog.youpay.digital/api/charge/payment")
  .method("POST", body)
  .addHeader("Content-Type", "application/json")
  .addHeader("idEstablishment", "<seu_establishment_id>")
  .addHeader("Accept", "application/json")
  .addHeader("Authorization", "Bearer <token_exemplo>")
  .build();
Response response = client.newCall(request).execute();
```

> Se certifique de trocar token_exemplo e seu_establishment_id pelos dados corretos.
> A requisição acima retorna um JSON estruturado desta forma:

```json
{
  "msg": "Pagamento processado",
  "details": "",
  "charge": {
    "id": "cdcfb95f-db3f-4318-9659-2c9e9e71997c",
    "description": "1151778/4 - Pagamento - novo anel",
    "obs": "1151778",
    "amount": "688.73",
    "id_establishment": "5bb8547a-d666-4b14-a9b4-843e173636bd",
    "type_transaction_installments": "FULL",
    "due_at": "2023-04-27T03:00:00.000000Z",
    "overdue": null,
    "paid_at": null,
    "paid": 0,
    "method_card_allow": 0,
    "method_pix_allow": 1,
    "method_boleto_allow": 1,
    "installments_max_allow": 1,
    "use_only_once": 1,
    "canceled_at": null,
    "canceled": 0,
    "enable": 1,
    "generated_api": null,
    "migrated_to_client_webhook": null,
    "amount_variable": null,
    "migrated_to_client_webhook_at": null,
    "id_user_created_charge": null,
    "aditional_info": null,
    "type_transaction": "NOW",
    "name_notification": "Gandalf, The White",
    "cellphone_notification": "8199999999",
    "email_notification": "gandalf@sociedade-do-anel.com",
    "discounts": "[{\"interest\": {\"value\": \"1.00\"}}, {\"fine\": {\"value\": \"2.00\"}}, {\"discount\": {\"type\": \"FIXED\", \"value\": \"135.00\", \"dueDateLimitDays\": 0}}]",
    "split": null,
    "is_donation": null,
    "enable_input_info_complement": null,
    "created_at": "2023-04-26T14:31:23.000000Z",
    "updated_at": "2023-04-26T14:31:23.000000Z",
    "deleted_at": null,
    "payments": []
  },
  "chargePayment": {
    "id_charge": "cdcfb95f-db3f-4318-9659-2c9e9e71997c",
    "amount": "688.73",
    "method": "bank_slip",
    "customer_name": "Frodo Bolseiro",
    "customer_document_type": "CPF",
    "customer_document": "69441700436",
    "customer_email": "frodo.bolseiro@sociedade-do-anel.com",
    "customer_phone": "8199999999",
    "info_complement": null,
    "updated_at": "2023-04-26T14:31:44.000000Z",
    "created_at": "2023-04-26T14:31:42.000000Z",
    "id": 1208,
    "boleto_raw": "{\"account\":null,\"data\":{\"object\":\"payment\",\"id\":\"pay_6516440196307917\",\"dateCreated\":\"2023-04-26\",\"customer\":\"cus_000005267983\",\"paymentLink\":null,\"value\":688.73,\"netValue\":686.74,\"originalValue\":null,\"interestValue\":null,\"description\":\"ID LINK PAGAMENTO: cdcfb95f-db3f-4318-9659-2c9e9e71997c\",\"billingType\":\"BOLETO\",\"canBePaidAfterDueDate\":true,\"pixTransaction\":null,\"status\":\"PENDING\",\"dueDate\":\"2023-04-27\",\"originalDueDate\":\"2023-04-27\",\"paymentDate\":null,\"clientPaymentDate\":null,\"installmentNumber\":null,\"invoiceUrl\":\"https:\\/\\/sandbox.asaas.com\\/i\\/6516440196307917\",\"invoiceNumber\":\"02417085\",\"externalReference\":\"cdcfb95f-db3f-4318-9659-2c9e9e71997c\",\"deleted\":false,\"anticipated\":false,\"anticipable\":false,\"creditDate\":null,\"estimatedCreditDate\":null,\"transactionReceiptUrl\":null,\"nossoNumero\":\"922245\",\"bankSlipUrl\":\"https:\\/\\/sandbox.asaas.com\\/b\\/pdf\\/6516440196307917\",\"lastInvoiceViewedDate\":null,\"lastBankSlipViewedDate\":null,\"discount\":{\"value\":135,\"limitDate\":null,\"dueDateLimitDays\":0,\"type\":\"FIXED\"},\"fine\":{\"value\":2,\"type\":\"PERCENTAGE\"},\"interest\":{\"value\":1,\"type\":\"PERCENTAGE\"},\"postalService\":false,\"identificationField\":\"23792693079000009222245000925607793330000068873\",\"refunds\":null},\"barcode\":\"23797933300000688732693090000092224500092560\",\"pix\":{\"qrCode\":\"iVBORw0KGgoAAAANSUhEUgAAAZAAAAGQCAIAAAAP3aGbAAAACXBIWXMAAA7EAAAOxAGVKw4bAAALEElEQVR4nO3dYW4iOxCF0WSU\\/S85egt4RjLjqSrf5pzfgQaSfGrJhf39+\\/v7BZDgz\\/QLANglWEAMwQJiCBYQQ7CAGIIFxBAsIIZgATEEC4ghWEAMwQJiCBYQQ7CAGIIFxBAsIIZgATEEC4ghWEAMwQJiCBYQQ7CAGIIFxBAsIIZgATEEC4ghWEAMwQJi\\/FQ86Z8\\/13Xw9\\/f35OGz72j54pcvqeJtzl59qeIlzX6ehw9\\/3n\\/cK9e9T4BXBAuIIVhADMECYggWEEOwgBglYw1LRcuc\\/7e\\/xHu46ny4Pr2v4uHLF384LlCxuN42VFHx3mdHEC78j\\/sH12q7EsAhwQJiCBYQQ7CAGIIFxBAsIEbfWMPS4YJo20r2UsW4wFLF+vTsCMK+2W0h9h1Ow7RNBsz+x51zhwXEECwghmABMQQLiCFYQAzBAmIMjzXMqljibVs2rthqYnZXidkzLCoudHj18RmCC7nDAmIIFhBDsIAYggXEECwghmABMT56rKHtNIGKYYW20xmWZncXmF3vnx1n+XDusIAYggXEECwghmABMQQLiCFYQIzhsYbZ1dzD8yaWDqcNDgcg9n+y4vyOfcuX1Lb\\/xOHkSsV7b\\/tHSJ+fcIcFxBAsIIZgATEEC4ghWEAMwQJi9I01tH2\\/\\/1DFFg7P+8mltrmEtnd0aPbzTPmPe8sD3xLwVIIFxBAsIIZgATEEC4ghWECMkrGGlG+Ez35Bf\\/8nKz7PlOc8vHrF2RAVv82KiZBHcocFxBAsIIZgATEEC4ghWEAMwQJilIw1pHwb\\/vA521adLzwKoeJXXLHdQsp6f8XbnN3ko4g7LCCGYAExBAuIIVhADMECYggWEKPvEIpD0Qu30ZMWbfMTy59sG5HZf50Vq\\/gVUyYpIx1vcYcFxBAsIIZgATEEC4ghWEAMwQJi3HgIxeFK9uxC+FLbiQ8VGx7sX33\\/J583O9K2fcXS7KRF51CFOywghmABMQQLiCFYQAzBAmIIFhCj7xCKtu0B2ladD6+eMpewVPErbntHFXMzs1sjVPx5t\\/3DvsUdFhBDsIAYggXEECwghmABMQQLiPH9vJ3qK\\/bzX6r45vqFD18a\\/9b+P1cxUHLhPMo+uzUAHBEsIIZgATEEC4ghWEAMwQJilIw1pKz7Pu91HprdwmF2ywEzGX\\/9cLs1ACwIFhBDsIAYggXEECwghmABMYZ3a2hbsG9TMRlwaPZUjn1t6+htQwD7V99\\/ztkPpOLhb7nurxbgFcECYggWEEOwgBiCBcQQLCDGT8WTti1zts0Q7C8wV2zdn7KrxNLs\\/MT+1ds+5MPPM2VIpcinvE\\/gAQQLiCFYQAzBAmIIFhBDsIAYJWMN+2bnEmYnLdqWt2d\\/cqltH4LZM1baLtT2NsdP5XCHBcQQLCCGYAExBAuIIVhADMECYpQcQtG2vF2xef7S7FfkL5xgmJWys8K+tr\\/kfXf+hbjDAmIIFhBDsIAYggXEECwghmABMUrGGpYqFm7bdhdYapuf2H\\/O2d0vDi904Ytv+1taahssaPvfPOcOC4ghWEAMwQJiCBYQQ7CAGIIFxCg5hGJ\\/ifdwMfjCWYeKC81+Rb5tyXx2qOLwQrP7eTzvQi9fwOzlAfYJFhBDsIAYggXEECwghmABMfp2a1i68Nvw+2ZfUtusw+xKdspQxfPOBGnby+Qt7rCAGIIFxBAsIIZgATEEC4ghWECM4bGGQ0Gb52+afUfROyvsu\\/Bwh4pf3NKFp4e89wLargRwSLCAGIIFxBAsIIZgATEEC4jRN9Ywvn39P\\/e87+LPnqTQNj8xu7PChZ\\/80p3jQU+LCPBgggXEECwghmABMQQLiCFYQIyfiied\\/eJ723NeeO5A27f2Kz75ivX+w5+s+B09b\\/eLTtmvHvgoggXEECwghmABMQQLiCFYQIySsYbZL6lfuAvCJz\\/n4Xr\\/obaJkNlxgbZJi\\/Eza9xhATEEC4ghWEAMwQJiCBYQQ7CAGCVjDfsqFoMrVl5njxhImcm4cPOMWW0vvu2TH591uO53DPCKYAExBAuIIVhADMECYggWEOO7bQhgKWXR+sKDAyr2DJjdh2D2\\/I6l2XNGZj\\/5fZ2zDu6wgBiCBcQQLCCGYAExBAuIIVhAjOGxhkOHUxEXriXPTjAsXbiJwoUDEEuzkxYVzzm+xYg7LCCGYAExBAuIIVhADMECYggWEOPGsYbZaYN9FUvmKTME+2YXwtuGACrMfvKz52K8cl0FAF4RLCCGYAExBAuIIVhADMECYpSMNSzNrrin7MGwFL0xw\\/M2pbjwbS7Nvvci7rCAGIIFxBAsIIZgATEEC4ghWECMvt0aLjzxYWn2S+oXbrewNDsE0ObCCYaKsyFmtxh5izssIIZgATEEC4ghWEAMwQJiCBYQ46fiSStWNCvGBfafc38xOHq9v211vG2cpe33XjFtsHThh9zpgW8JeCrBAmIIFhBDsIAYggXEECwgRslYw9LzVrIPVVxo9nUefsj7ZhfsK2Yd9h\\/eNt9z4eYZX+6wgCCCBcQQLCCGYAExBAuIIVhAjL6xhtmjECoefrhovf+c+9rGBdLPMhjUNs7StgNE5+\\/IHRYQQ7CAGIIFxBAsIIZgATEEC4gxvFvD7EkK0VKOQtg3e1THhZt8VHzIhy9pfNbhI\\/63gWcQLCCGYAExBAuIIVhADMECYvSNNeybXWCeXbA\\/fM7Dn6yYCJmdMmnbJ+NQ9PiF3RoAFgQLiCFYQAzBAmIIFhBDsIAY37NnQ1R8w35pdml\\/X9vBARXalrfbthy4UNt\\/x50nU2T8kgC+BAsIIlhADMECYggWEEOwgBglYw1Ls4cm7L+kwwvNHoWQ8vC2mYwL\\/8AqXtKFv7gi7rCAGIIFxBAsIIZgATEEC4ghWECMGw+haPs+ettUxP7DZ5eiP2TJfHZLjJRtIZbGZx2CPzvg0wgWEEOwgBiCBcQQLCCGYAExhsca2uYSZr83P3sqR9vD981OhBw+5+ygxvh+CbNXd4cFxBAsIIZgATEEC4ghWEAMwQJilBxCUXFwwOHV2w44qNB2EEPFp7Sv7U\\/xwr\\/5WeN7MOwL\\/pSBTyNYQAzBAmIIFhBDsIAYggXEKNmtIfq74xVHYBy6cM7jwvM72lR8SrOf\\/IUHhbziDguIIVhADMECYggWEEOwgBiCBcQoGWu48JvrbSuvsyMdF673z46JfMiv4\\/CTP\\/zJzlmH68oC8IpgATEEC4ghWEAMwQJiCBYQo2SsYenCIxsOV9wrNjyYXQg\\/VLFPxuy+DsuXNPtns3Thfh5F3GEBMQQLiCFYQAzBAmIIFhBDsIAYfWMNSxeu5lZc6HnnYlx4AEfbQMns5ErbPMqdsw7usIAYggXEECwghmABMQQLiCFYQIzhsYYLte3BsL8TwIXDHxU7Fhy+pEMVRzYcPrxtsKDtDItz7rCAGIIFxBAsIIZgATEEC4ghWEAMYw1\\/r2Ldd3bLgYozFyo870CTw+e8cEykSMwLBRAsIIZgATEEC4ghWEAMwQJiDI81dH7Pe1PFZMC+2b0iDi\\/Uti1E27RB2+YZy+c8fEmzwx9FV3eHBcQQLCCGYAExBAuIIVhADMECYvSNNaR8I7xi2bht3ffCyYB9bbtfHB7\\/MXtQyIXDNJ1ufE0AS4IFxBAsIIZgATEEC4ghWECM7wv3SwBYcocFxBAsIIZgATEEC4ghWEAMwQJiCBYQQ7CAGIIFxBAsIIZgATEEC4ghWEAMwQJiCBYQQ7CAGIIFxBAsIIZgATEEC4ghWEAMwQJiCBYQQ7CAGIIFxBAsIIZgATEEC4jxH7xG8ru8jFTnAAAAAElFTkSuQmCC\",\"key\":\"00020101021226820014br.gov.bcb.pix2560qrpix-h.bradesco.com.br\\/9d36b84f-c70b-478f-b95c-12729b90ca255204000053039865406553.735802BR5905ASAAS6009JOINVILLE62070503***63046106\",\"externalid\":\"pay_6516440196307917\"}}",
    "customer_street": "Rua dos Bolseiros",
    "customer_number": "9",
    "customer_complement": null,
    "customer_district": "Condadinho",
    "customer_city": "Condado",
    "customer_state": "Middle-Earth",
    "customer_country": "Brasil",
    "customer_postal_code": "9000000"
  },
  "methods": {
    "account": null,
    "data": {
      "object": "payment",
      "id": "pay_6516440196307917",
      "dateCreated": "2023-04-26",
      "customer": "cus_000005267983",
      "paymentLink": null,
      "value": 688.73,
      "netValue": 686.74,
      "originalValue": null,
      "interestValue": null,
      "description": "ID LINK PAGAMENTO: cdcfb95f-db3f-4318-9659-2c9e9e71997c",
      "billingType": "BOLETO",
      "canBePaidAfterDueDate": true,
      "pixTransaction": null,
      "status": "PENDING",
      "dueDate": "2023-04-27",
      "originalDueDate": "2023-04-27",
      "paymentDate": null,
      "clientPaymentDate": null,
      "installmentNumber": null,
      "invoiceUrl": "https://sandbox.asaas.com/i/6516440196307917",
      "invoiceNumber": "02417085",
      "externalReference": "cdcfb95f-db3f-4318-9659-2c9e9e71997c",
      "deleted": false,
      "anticipated": false,
      "anticipable": false,
      "creditDate": null,
      "estimatedCreditDate": null,
      "transactionReceiptUrl": null,
      "nossoNumero": "922245",
      "bankSlipUrl": "https://sandbox.asaas.com/b/pdf/6516440196307917",
      "lastInvoiceViewedDate": null,
      "lastBankSlipViewedDate": null,
      "discount": {
        "value": 135,
        "limitDate": null,
        "dueDateLimitDays": 0,
        "type": "FIXED"
      },
      "fine": {
        "value": 2,
        "type": "PERCENTAGE"
      },
      "interest": {
        "value": 1,
        "type": "PERCENTAGE"
      },
      "postalService": false,
      "identificationField": "23792693079000009222245000925607793330000068873",
      "refunds": null
    },
    "barcode": "23797933300000688732693090000092224500092560",
    "pix": {
      "qrCode": "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",
      "key": "00020101021226820014br.gov.bcb.pix2560qrpix-h.bradesco.com.br/9d36b84f-c70b-478f-b95c-12729b90ca255204000053039865406553.735802BR5905ASAAS6009JOINVILLE62070503***63046106",
      "externalid": "pay_6516440196307917"
    }
  },
  "bankInfo": {
    "agency": "0001",
    "account": "1413541",
    "accountDigit": "2",
    "bankCode": 461,
    "bankName": "ASAAS"
  }
}
```

Todas as cobranças geradas pela API da Youpay podem ser pagas via Cartão de Crédito, Pix e/ou Boleto Bancário, dependendo da forma como a cobrança foi configurada na hora da criação.

### Requisição HTTP

`POST http://homolog.youpay.digital/api/charge/payment`

Dependendo da forma de pagamento escolhida, informações diferentes devem ser enviadas no corpo da requisição. Mas os campos abaixo serão sempre obrigatórios.

### Corpo da requisição

| Parâmetro                                   | Descrição                            | Tipo   |
| ------------------------------------------- | ------------------------------------ | ------ |
| method <sub>Obrigatório</sub>               | Método de pagamento escolhido        | String |
| customerName <sub>Obrigatório</sub>         | Nome do cliente pagante              | String |
| customerDocument <sub>Obrigatório</sub>     | Documento do cliente pagante         | String |
| customerTypeDocument <sub>Obrigatório</sub> | Tipo do documento do cliente pagante | String |
| idCharge <sub>Obrigatório</sub>             | Identificador da cobrança a ser paga | String |

### Campos opcionais

Além dos campos obrigatórios mostrados anteriormente, é possível também passar os seguintes campos (necessários para alguns pagamentos).

| Parâmetro          | Descrição                                                                                          | Tipo   |
| ------------------ | -------------------------------------------------------------------------------------------------- | ------ |
| customerNumber     | Número do endereço fiscal do cliente pagante                                                       | String |
| customerStreet     | Rua do endereço fiscal do cliente pagante                                                          | String |
| customerDistrict   | Bairro do endereço fiscal do cliente pagante                                                       | String |
| customerCity       | Cidade do endereço fiscal do cliente pagante                                                       | String |
| customerState      | Estado do endereço fiscal do cliente pagante                                                       | String |
| customerPostalCode | CEP do endereço fiscal do cliente pagante                                                          | String |
| amountVariable     | Valor do pagamento (apenas quando a cobrança aceita pagamentos com valores diferentes do original) | String |

### Pagando com Boletos Bancários

Para realizar o pagamento via Boleto Bancário é necessário apenas passar o campo `method` como `bank_slip` no corpo da requisição.

<aside class="notice">
É importante lembrar que os pagamentos via Boleto Bancário podem demorar até 3 dias úteis para serem processados.
</aside>

### Pagando com Pix

Para realizar o pagamento via Pix é necessário apenas passar o campo `method` como `pix` no corpo da requisição.

Em pagamentos de **cobranças que aceitam valores diferentes** do original, **não é possível realizar um pix de menos de R$5,00**. Caso tente realizar essa operação, você receberá um erro [400 (Bad Request)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/400).

## Pagando com cartão de crédito

Para pagamentos via cartão de crédito, existem alguns caminhos possíveis.

- Passar os dados do cartão no corpo da requisição;
- Passar o token do cartão, gerado no processo de [tokenização do cartão](#tokenizacao-do-cartao).

### Passando os dados do cartão

Além dos campos obrigatórios e opcionais já comentados anteriormente, é necessário agora enviar as informações a seguir:

| Parâmetro                           | Descrição                                   | Tipo   |
| ----------------------------------- | ------------------------------------------- | ------ |
| numberCard <sub>Obrigatório</sub>   | Número do cartão                            | String |
| nameCard <sub>Obrigatório</sub>     | Nome do portador do cartão                  | String |
| expiryCard <sub>Obrigatório</sub>   | Data de validade do cartão no formato MM/AA | String |
| cvcCard <sub>Obrigatório</sub>      | Código verificador do cartão                | String |
| installments <sub>Obrigatório</sub> | Quantidade de parcelas                      | String |

### Passando o token do cartão

Após passar pelo processo de [tokenização do cartão](#tokenizacao-do-cartao), é possível enviar apenas o token gerado no corpo da requisição, além dos campos [obrigatórios](#realizando-um-pagamento) e [opcionais](#campos-opcionais).

| Parâmetro                        | Descrição                              | Tipo   |
| -------------------------------- | -------------------------------------- | ------ |
| tokenCard <sub>Obrigatório</sub> | Token gerado para identificar o cartão | String |

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

> O identificador da cobrança não foi encontrado

```json
{
  "msg": "desculpe",
  "details": "O id da cobrança informado não existe"
}
```

> Já existe um pagamento em aberto e a cobrança não aceita mais

```json
{
  "msg": "Desculpe!",
  "details": "Identificamos que já existe um pagamento no <método_de_pagamento> em andamento, no valor de R$XXX,XX"
}
```

> Houve uma tentativa de pagamento com um meio não suportado pela cobrança

```json
{
  "msg": "Desculpe!",
  "details": "Você tentou pagar um método de pagamento não permitido"
}
```

> Pagamento de menos de R$5,00 via Pix em cobranças configuradas para valor variável

```json
{
  "msg": "Desculpe!",
  "details": "Não é possível realizar pagamentos menores que R$5,00 em pix."
}
```

Caso algum campo não seja preenchido corretamente, você pode se deparar com algum erro na hora de realizar a requisição.

Ao lado estão alguns errors comuns e suas causas.

De maneira geral, os erros de pagamento de cobranças seguem o seguinte padrão:

| Campo   | Descrição                           | Tipo   |
| ------- | ----------------------------------- | ------ |
| msg     | Uma mensagem sobre o erro           | String |
| details | Mais detalhes sobre a causa do erro | String |

Além desse padrão de respostas, os [status HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) utilizados nos casos de erro também visam ajudá-lo a entender o que pode ter ocorrido, abaixo está uma lista de status utilizados nesse fluxo e o que podem significar:

| Código | Nome                  | Descrição                                                                                               |
| ------ | --------------------- | ------------------------------------------------------------------------------------------------------- |
| 400    | Bad Request           | Alguma informação na requisição não segue o padrão desejado, olhe a mensagem de erro para mais detalhes |
| 404    | Not Found             | Identificador da cobrança não encontrado                                                                |
| 422    | Unprocessable Content | Alguma informação obrigatória não foi fornecida no corpo da requisição                                  |
