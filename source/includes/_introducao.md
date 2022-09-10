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

CÓDIGO | DESCRIÇÃO                | SITUAÇÃO
-------|--------------------------|-----------------------------------------------
200    | *OK*                     | Requisição atendida com sucesso
201    | *Created*                | Registro criado (geralmente em método POST /recurso)
204    | *No Content*             | Registro alterado ou excluído (geralmente em método PATCH ou DELETE /recurso)
401    | *Unauthorized*           | Token ausente, expirado ou não autorizado
403    | *Forbidden*              | Acesso proibido ao recurso requisitado (usuário sem permissão)
404    | *Resource Not Found*     | Registro ou recurso não encontrado
422    | *Unprocessable Entity*   | Quando ocorrer erros de validação, como, um campo obrigatório não informado
429    | *Too Many Requests*      | Excedeu o seu limite de requisições por minuto
500    | *Internal Server Error*  | Quando ocorrer um erro interno no recurso da API
502    | *Bad Gateway*            | Sistema em atualização, voltaremos em poucos segundos
503    | *Service Unavailable*    | No momento estamos offline para manutenção no sistema, tente mais tarde

# Token de Acesso

Para obter o token de acesso às nossas APIs, solicite pelo e-mail <a href="mailto:suporte@securities.com.br">suporte@securities.com.br</a>.

<aside class="notice">O token de acesso é liberado somente para contas cadastradas na Securities</aside>
