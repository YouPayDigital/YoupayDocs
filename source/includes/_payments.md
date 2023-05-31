# Pagamentos

## Realizando um pagamento

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
- Passar o token do cartão, gerado no processo de [tokenização do cartão](#).

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

Após passar pelo processo de [tokenização do cartão](#), é possível enviar apenas o token gerado no corpo da requisição, além dos campos [obrigatórios](#realizando-um-pagamento) e [opcionais](#campos-opcionais).

| Parâmetro                        | Descrição                              | Tipo   |
| -------------------------------- | -------------------------------------- | ------ |
| tokenCard <sub>Obrigatório</sub> | Token gerado para identificar o cartão | String |
