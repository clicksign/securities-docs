# Migração da Antiga Securities

Trata-se de uma API transitória, para que nossos atuais clientes Clicksign Securities possam se planejar para refazer a conexão de API atual, mesmo assim, usufruindo da nova plataforma Clicksign Securities com suas novas features, melhor performance e maior escalabilidade.

Para os clientes atuais, essa API de compatibilidade vai funcionar como uma ponte para conectá-lo da API legada (atual deste cliente) até a Nova Clicksign Securities, realizando a conversão dos formatos que os dados são enviados para o formato que a Nova Securities espera receber.

Para novos clientes, a conexão com a nova Securities deve se dar pela criação da conexão da Nova API. Para os atuais clientes, o uso da API de compatibilidade será uma aceleração para usufruir do novo produto, sem maiores esforços de desenvolvimento inicial.

É importante ressaltar que novas features serão lançadas a partir de abril/2023 apenas para a nova API, o que nos leva a reforçar que após conectar a API de compatibilidade com esforço mínimo, o planejamento para conectar-se com a nova API é essencial para garantir que todos terão acesso aos lançamentos futuros.

## Mudanças importantes nas integrações

Para os clientes que vierem do Securities Legado, provavelmente, os documentos de CCBs estão sendo criados diretamente na plataforma de assinatura da Clicksign através das API fornecidas pela plataforma de assinatura e não pela API do sistema de securitização.

No novo Securities será diferente, disponibilizamos algumas APIs de compatibilidade para a criação das CCBs, dessa forma, toda a comunicação via API deverá ser com o novo sistema. Essa mudança foi feita porque todas as informações sobre os documentos, bem como as assinaturas pendentes e realizadas e o arquivo PDF estarão disponíveis nas novas APIs do novo Securities, portanto, não será necessário acessar a interface gráfica da plataforma de assinatura da Clicksign para localizar os documentos das CCBs, endossos referenciado ou dos termos de cessão.

É importante ressaltar que, todos os documentos assinados serão baixados para o Securities e vinculados aos registros de cada operação, tornando possível a visualização de cada um desses documentos dentro de suas respectivas operações, ou seja, quando pesquisar por uma CCB utilizando as novas APIs, será possível obter todos os documentos relacionados a ela.

<aside class="warning">
  Os endpoints descritos nessa seção tem o único intuito de manter compatibilidade com os sistemas de clientes antigos e não devem ser utilizados em novas integrações.
</aside>

## Criar proposta (Legado)

> Request:

```shell
curl -X POST https://app.securities.com.br/api/legacy/proposals \
   -H "Authorization: Bearer $TOKEN" \
   -H "Content-Type: application/json" \
   -d '{
          "proposal": {
            "template_key": "e7c3534c-2b04-11ed-a261-02422b00ac13",
            "document_data": {
              "number": 231387,
              "issuer_full_name": "Hugo Fonseca",
              "issuer_full_address": "Setor M QNM 03 Conjunto Z - 72200-000, Brasília - DF",
              "issuer_cpf": "657.565.000-73",
              "issuer_rg": "47.825.277-8",
              "issuer_cnh": "81457959115",
              "issuer_email": "hugo@email.com",
            }
          }
        }'
```

> Response:

```shell
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
```

```json
{
  "proposal": {
    "template_key": "e7c3534c-2b04-11ed-a261-02422b00ac13",
    "document_data": {
      "number": 231387,
      "issuer_full_name": "Hugo Fonseca",
      "issuer_full_address": "Setor M QNM 03 Conjunto Z - 72200-000, Brasília - DF",
      "issuer_cpf": "657.565.000-73",
      "issuer_rg": "47.825.277-8",
      "issuer_cnh": "81457959115",
      "issuer_email": "hugo@email.com"
    },
    "document": {
      "id": 25,
      "key": "f91e734e-ad1e-42f4-b12f-755e67178929",
      "status": "validated",
      "created_at": "2022-12-21T02:41:28.748Z",
      "updated_at": "2022-12-21T02:41:28.748Z",
      "file": "https://example.com/path/to/document.pdf"
    }
  }
}
```

Esse endpoint cria uma proposta

`POST https://app.securities.com.br/api/legacy/proposals`

| Parâmetro     | Obrigatório | Tipo   | Descrição                               |
| ------------- | ----------- | ------ | --------------------------------------- |
| template_key  | sim         | string | Chave do template no assinador          |
| document_data | sim         | json   | Dados do documento para compor o título |

## Buscar contrato (CCB) existente

> Request:

```shell
curl -X GET https://app.securities.com.br/api/legacy/securities/:id \
   -H "Authorization: Bearer $TOKEN" \
   -H "Content-Type: application/json"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "id": 2,
  "process": 3,
  "number": 231387,
  "issuer_cpf": "657.565.000-73",
  "issuer_full_name": "Hugo Fonseca",
  "parcels": 5,
  "first_installment_due_date": "2022-12-01",
  "last_installment_due_date": "2023-12-01",
  "parcels_value": 200.0,
  "today_value": 160.0,
  "leasing_total_value": 192.0,
  "cession_value": 180.0,
  "metadata": {
    // Todos os dados do modelo
  }
}
```

Esse endpoint obtém todos os dados de uma CCB

`GET https://app.securities.com.br/api/legacy/securities/:id`

| Parâmetro | Obrigatório | Tipo    | Descrição               |
| --------- | ----------- | ------- | ----------------------- |
| id        | sim         | integer | Chave da security (CCB) |

## Buscar lote existente (assignments)

> Request:

```shell
curl -X GET https://app.securities.com.br/api/legacy/assignments/:id \
   -H "Authorization: Bearer $TOKEN" \
   -H "Content-Type: application/json"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "process": 3,
  "status": "pending",
  "cession_number": 442142,
  "cession_value": 1877.99,
  "cession_parcels": 30,
  "cession_contracts": 2,
  "assignor": 7,
  "transferee": 8,
  "contracts": [231387, 231388]
}
```

Esse endpoint obtém todos os dados de lote de CCB

`GET https://app.securities.com.br/api/legacy/assignments/:id`

| Parâmetro | Obrigatório | Tipo    | Descrição                          |
| --------- | ----------- | ------- | ---------------------------------- |
| id        | sim         | integer | Chave do lote de CCBs (assignment) |

## Cancelar lote existente

> Request:

```shell
curl -X POST https://app.securities.com.br/api/legacy/assignments/:id/cancel \
   -H "Authorization: Bearer $TOKEN" \
   -H "Content-Type: application/json"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "process": 3,
  "status": "canceling",
  "cession_number": 442142,
  "cession_value": 1877.99,
  "cession_parcels": 30,
  "cession_contracts": 2,
  "assignor": 7,
  "transferee": 8,
  "contracts": [231387, 231388]
}
```

Esse endpoint cancela um lote de cessão de CCBs

<aside class="notice">
O cancelamento é permitido até 2 dias após a cessão
</aside>

`POST https://app.securities.com.br/api/legacy/assignments/:id/cancel`

| Parâmetro | Obrigatório | Tipo    | Descrição                          |
| --------- | ----------- | ------- | ---------------------------------- |
| id        | sim         | integer | Chave do lote de CCBs (assignment) |

## Criar Signatário (Legado)

> Request:

```shell
curl -X POST https://app.securities.com.br/api/legacy/signers \
   -H "Authorization: Bearer $TOKEN" \
   -H "Content-Type: application/json" \
    -d '{
          "signer": {
            "email": "fulano@example.com",
            "auth": "email",
            "full_name": "Marcos Zumba",
            "has_documentation": true,
            "documentation": "123.321.123-40",
            "birthday": "1983-03-31",
            "phone_number": "11999999999",
            "sign_as": "sign",
            "communicate_by": "email",
            "selfie_enabled": false,
            "facial_biometrics_enabled": false,
            "handwritten_enabled": false,
            "official_document_enabled": false,
            "liveness_enabled": false
          }
        }'
```

> Response:

```shell
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
```

```json
{
  "signer": {
    "id": 4,
    "full_name": "Marcos Zumba",
    "has_documentation": true,
    "documentation": "123.321.123-40",
    "email": "fulano@example.com",
    "birthday": "1983-03-31",
    "phone_number": "11999999999",
    "auth": "email",
    "communicate_by": "email",
    "key": null,
    "sign_as": "sign",
    "created_at": "2022-09-16T18:41:00.079-03:00",
    "updated_at": "2022-09-16T18:41:00.079-03:00",
    "selfie_enabled": false,
    "facial_biometrics_enabled": false,
    "handwritten_enabled": false,
    "official_document_enabled": false,
    "liveness_enabled": false
  }
}
```

Esse endpoint cria um signatário

`POST https://app.securities.com.br/api/legacy/signers`

| Parâmetro                 | Obrigatório | Tipo    | Descrição                                                     |
| ------------------------- | ----------- | ------- | ------------------------------------------------------------- |
| full_name                 | sim         | string  | Nome completo                                                 |
| has_documentation         | não         | boolean | Tem documentação, como CPF, CNPJ ou Passaporte. Padrão é TRUE |
| documentation             | condicional | string  | CPF, CNPJ ou Passaporte                                       |
| birthday                  | condicional | string  | Data de nascimento                                            |
| email                     | condicional | string  | E-mail                                                        |
| phone_number              | sim         | string  | Numero de telefone                                            |
| auth                      | sim         | string  | Tipo de autenticação: "email" ou "api"                        |
| communicate_by            | sim         | string  | Por onde será notificado: "email"                             |
| sign_as                   | sim         | string  | Assinar como: sign, party, witness, contractor, contractee... |
| selfie_enabled            | não         | boolean | Padrão é FALSE                                                |
| facial_biometrics_enabled | não         | boolean | Padrão é FALSE                                                |
| handwritten_enabled       | não         | boolean | Padrão é FALSE                                                |
| official_document_enabled | não         | boolean | Padrão é FALSE                                                |
| liveness_enabled          | não         | boolean | Padrão é FALSE                                                |

## Vincular Signatário ao documento

> Request:

```shell
curl -X POST https://app.securities.com.br/api/legacy/signers/signer_id:/lists \
   -H "Authorization: Bearer $TOKEN" \
   -H "Content-Type: application/json" \
    -d '{
          "list": {
            "document_id": 1,
            "group": null,
            "message": null,
            "refusable": false,
          }
        }'
```

> Response:

```shell
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
```

```json
{
  "list": {
    "id": 4,
    "document_id": 1,
    "signer_id": 4,
    "created_at": "2022-09-16T18:41:00.079-03:00",
    "updated_at": "2022-09-16T18:41:00.079-03:00",
    "group": null,
    "message": null,
    "refusable": false
  }
}
```

Esse endpoint Vincula um signatário a um documento

`POST https://app.securities.com.br/api/legacy/signers/:signer_id/lists`

| Parâmetro   | Obrigatório | Tipo    | Descrição                                                                                                                                                                |
| ----------- | ----------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| document_id | sim         | integer | Chave única do documento dentro do Securities                                                                                                                            |
| group       | não         | integer | Determina o grupo que o signatário deve ser vinculado. Deve ser número, inteiro e maior que 0. Não adicione esse parâmetro caso não deseje uma ordenação de assinaturas. |
| message     | não         | string  | Mensagem que será enviada no body do e-mail de solicitação de assinatura aos signatários. O parâmetro funciona com sequence_enabledcomo true e group é obrigatório       |
| refusable   | não         | boolean | Padrão é FALSE                                                                                                                                                           |

## Criar um processo de cessão

> Request:

```shell
curl -X POST https://app.securities.com.br/api/legacy/assignments\
   -H "Authorization: Bearer $TOKEN" \
   -H "Content-Type: application/json" \
    -d '{
          "cession_number": "123456789",
          "cession_value": 1000,
          "cession_parcels": 1,
          "cession_contracts": 30,
          "issue_date": "2021-09-16",
          "arrangement": 1,
          "callback_url": "https://example.com/callback"
        }'
```

> Response:

```shell
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
```

```json
{
  "process": "123456789",
  "status": "pending"
}
```

Esse endpoint cria um processo de cessão

`POST https://app.securities.com.br/api/legacy/assignments`

| Parâmetro        | Obrigatório | Tipo    | Descrição                                    |
|------------------| ----------- | ------- |----------------------------------------------|
| cession_number   | sim         | string  | Número da cessão                             |
| cession_value    | sim         | integer | Valor da cessão                              |
| cession_parcels  | sim         | integer | Quantidade de parcelas negociadas na cessão  |
| cession_contracts | sim         | integer | Quantidade de contratos negociados na cessão |
| issue_date       | sim         | string  | Data de emissão da cessão                    |
| arrangement      | sim         | integer | ID do Arranjo                                |
| callback_url     | não         | string  | URL de callback                              |

## Executar um processo de cessão

> Request:

```shell
curl -X POST https://app.securities.com.br/api/legacy/contracts\
   -H "Authorization: Bearer $TOKEN" \
   -H "Content-Type: application/json" \
    -d '{
          "process": "123",
          "contracts": [
            { "number": "123456789", issuer_name: "Issuer Name"... },
            { "number": "125468797", issuer_name: "Issuer Name"... }
          ]
        }'
```

> Response:

```shell
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
```

```json
{
  "status": "accepted"
}
```

Esse endpoint Executa um processo de cessão

`POST https://app.securities.com.br/api/legacy/contracts`

| Parâmetro | Obrigatório | Tipo    | Descrição                |
| --------- | ----------- | ------- | ------------------------ |
| process   | sim         | Integer | ID do processo de cessão |
| contracts | sim         | Array   | Array de contratos       |
