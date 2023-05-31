# Pagamentos

## Realizando um pagamento

Todas as cobranças geradas pela API da Youpay podem ser pagas via Cartão de Crédito, Pix e/ou Boleto Bancário, dependendo da forma como a cobrança foi configurada na hora da criação.

### Requisição HTTP

`POST http://homolog.youpay.digital/api/charge/payment`

Dependendo da forma de pagamento escolhida, informações diferentes devem ser enviadas no corpo da requisição.

### Pagando com Boletos Bancários

aa
