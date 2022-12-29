# Introdução

Disponibilizamos essa API com o intuito de fornecer acesso aos recursos da Securities por meio da arquitetura REST, dessa forma, você poderá fazer uso dos recursos do nosso sistema fora do nosso ambiente UI, e com isso, contextualizar melhor as funcionalidades dentro da sua necessidade.

# Visão geral

O objetivo desta documentação é orientar o desenvolvedor sobre como integrar com o SECURITIES-API, descrevendo as funcionalidades, os métodos a serem utilizados, listando informações a serem enviadas e recebidas, e provendo exemplos.

O mecanismo de integração com o SECURITIES-API é simples, de modo que apenas conhecimentos intermediários em linguagem de programação para Web, requisições HTTP/HTTPS e manipulação de arquivos JSON são necessários para integrar com o SECURITIES-API.

Nesse manual você encontrará a referência sobre todas as operações disponíveis no SECURITIES-API. As operações devem ser executadas utilizando um token de acesso obtido através do recurso de autenticação. Esse token é gerado com base em uma organização ativa na Securities.

Disponibilizamos abaixo as urls de acesso aos nossos ambientes:

**Ambiente Produção:** https://api.securities.com.br

**Ambiente Homologação:** https://api-staging.securities.com.br

# Códigos de status

No SECURITIES-API, os status de retorno das requisições devem ser esperados conforme especificado nas situações abaixo:

| CÓDIGO | DESCRIÇÃO               | SITUAÇÃO                                                                      |
| ------ | ----------------------- | ----------------------------------------------------------------------------- |
| 200    | _OK_                    | Requisição atendida com sucesso                                               |
| 201    | _Created_               | Registro criado (geralmente em método POST /recurso)                          |
| 204    | _No Content_            | Registro alterado ou excluído (geralmente em método PATCH ou DELETE /recurso) |
| 401    | _Unauthorized_          | Token ausente, expirado ou não autorizado                                     |
| 403    | _Forbidden_             | Acesso proibido ao recurso requisitado (usuário sem permissão)                |
| 404    | _Resource Not Found_    | Registro ou recurso não encontrado                                            |
| 422    | _Unprocessable Entity_  | Quando ocorrer erros de validação, como, um campo obrigatório não informado   |
| 429    | _Too Many Requests_     | Excedeu o seu limite de requisições por minuto                                |
| 500    | _Internal Server Error_ | Quando ocorrer um erro interno no recurso da API                              |
| 502    | _Bad Gateway_           | No momento estamos offline para manutenção no sistema, tente mais tarde       |
| 503    | _Service Unavailable_   | No momento estamos offline para manutenção no sistema, tente mais tarde       |

# Token de Acesso

Para obter o token de acesso às nossas APIs, solicite pelo e-mail <a href="mailto:suporte@securities.com.br">suporte@securities.com.br</a>.

<aside class="notice">O token de acesso é liberado somente para contas cadastradas na Securities</aside>
