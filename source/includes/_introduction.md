# Introdução

A API de cobranças da Youpay, está implementada em conformidade com o princípio de
design REST.

Essa API possui recursos orientados a URLs, com códigos HTTP para indicar erros. Ela utiliza também funcionalidades HTTP nativas, como verbos
de ação POST, PUT, GET, DELETE, para operações de leitura e escrita, bem
como o modelo básico de autenticação HTTP.

Há ainda o suporte de chamadas diretas aos recursos da API a partir de outras origens - CORS (cross-origin resource sharing) - permitindo você interagir de maneira segura com a API a partir de aplicações web.

Todas as respostas da API estão no formato de dados JSON, incluindo errors.

Durante o restante da documentação todos os exemplos utilizarão a URL do nosso ambiente de homologação `https://homolog.youpay.digital`. Sinta-se a vontade para testar suas requisições nesse ambiente e, quando estiver pronto, mudar para o ambiente de produção `https://app.youpay.digital`.
