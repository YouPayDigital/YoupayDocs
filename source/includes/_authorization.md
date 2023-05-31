# Autorização

Após receber seu [token de autenticação](#gerando-um-token), é esperado que você o utilize no cabeçalho das próximas requisições da seguinte maneira:

`Authorization: <token_exemplo>`

<aside class="notice">
Você deve substituir <code>token_exemplo</code> pelo seu token.
</aside>

Esse padrão segue a [especificação de códigos de autorização](https://oauth.net/2/grant-types/authorization-code/) do OAuth2.

Além disso, os tokens possuem uma data de expiração, portanto, é esperado que você os gere de forma dinâmica na sua aplicação.

<aside class="warning">
Seu token de autenticação carrega muitos privilégios e dados sensíveis, se certifique de guardá-lo em um local seguro! Nunca compartilhe seus tokens em áreas públicas como Github, código client-side, etc.
</aside>
