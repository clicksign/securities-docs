# API Legada

<aside class="notice">
Os endpoint descritos nessa seção tem o único intuito de manter compatibilidade com os sistemas de clientes antigos e não devem ser utilizados em novas integrações.
</aside>

## Criar proposta

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
      "issuer_email": "hugo@email.com",
    }
  }
}
```

Esse endpoint cria uma proposta

### HTTP Request

`POST https://app.securities.com.br/api/legacy/proposals`

### Parâmetros da requisição

| Parâmetro       | Obrigatório | Tipo    | Descrição                               |
| --------------- | ----------- | ------- | --------------------------------------- |
| template_key    | sim         | string  | Chave do template no assinador          |
| document_data   | sim         | json    | Dados do documento para compor o título |

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
  "parcels_value": 200.00,
  "today_value": 160.00,
  "leasing_total_value": 192.00,
  "cession_value": 180.00,
  "metadata": {
    // Todos os dados do modelo
  }
}
```

Esse endpoint obtém todos os dados de uma CCB

### HTTP Request

`GET https://app.securities.com.br/api/legacy/securities/:id`

### Parâmetros da requisição

| Parâmetro       | Obrigatório | Tipo    | Descrição                               |
| --------------- | ----------- | ------- | --------------------------------------- |
| id              | sim         | integer | Chave da security (CCB)                 |

## Criar Signatário

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

### HTTP Request

`POST https://app.securities.com.br/api/legacy/signers`

### Parâmetros da requisição

| Parâmetro                 | Obrigatório | Tipo    | Descrição                                                     |
|---------------------------| ----------- | ------- | ------------------------------------------------------------- |
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
