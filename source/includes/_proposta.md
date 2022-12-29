# Proposta

A proposta é o documento que representa a CCB antes dela ser assinada pelo tomador. Enquanto o tomador não assina o documento, ele ainda não se tornou uma CCB para ser cedida, então esse documento é uma Proposta de se tornar uma CCB.

A proposta conterá todos os dados de uma CCB, seguindo o modelo preconizado entre originador e fundo, entretanto, o que o diferencia de uma CCB é o fato de ainda não estar assinado pelo tomador.

## Listar propostas

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/proposals \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "proposals": [
    {
      "id": 218,
      "number": "123456",
      "issuer_full_name": "Hugo Fonseca",
      "issuer_document": "882.793.334-44",
      "installments": 48,
      "created_at": "2022-10-07T12:00:33.571-03:00",
      "updated_at": "2022-10-07T12:00:33.571-03:00"
    }
  ],
  "page_infos": {
    "total_pages": 3,
    "current_page": 1,
    "next_page": 2,
    "prev_page": null,
    "first_page?": true,
    "last_page?": false
  }
}
```

Esse endpoint lista todas as propostas

### HTTP Request

`GET https://app.securities.com.br/api/v1/proposals`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| page      | integer | Paginação |

## Obter proposta

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/proposals/:id \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "proposal": {
    "id": 3073,
    "number": "123321",
    "issuer_full_name": "Hugo Fonseca",
    "issuer_document": "882.793.334-44",
    "installments": 48,
    "created_at": "2022-10-27T09:44:50.772-03:00",
    "updated_at": "2022-10-27T09:44:50.772-03:00",
    "document_data": {
      "number": 231387,
      "issuer_full_name": "Hugo Fonseca",
      "issuer_full_address": "Setor M QNM 03 Conjunto Z - 72200-000, Brasília - DF",
      "issuer_cpf": "657.565.000-73",
      "issuer_rg": "47.825.277-8",
      "issuer_cnh": "81457959115",
      "issuer_email": "hugo@email.com",
      "guarantor_full_name": "Juan Isaac Fogaça",
      "guarantor_cpf": "822.448.901-98",
      "guarantor_rg": "34.576.797-4",
      "guarantor_full_address": "Quadra Quadra 300 Conjunto 31 - 72260-132, Brasília - DF",
      "financed_amount": 125314.12,
      "bank_name": "341 - Banco Itaú",
      "bank_agency_number": 7957,
      "bank_account_number": 423762,
      "disbursed_amount": 108323.45,
      "tac": 42.89,
      "pmt": 2784.12,
      "maturity": 60,
      "ccb_registration_fee": 88.32,
      "first_installment_due_date": "31/10/2022",
      "last_installment_due_date": "31/10/2027",
      "iof": 43.21,
      "commercial_yearly_interest_rate": 13.42,
      "commercial_monthly_interest_rate": 2.21,
      "cet_yearly_rate": 21.32,
      "cet_monthly_rate": 9.87
    },
    "document": {
      "id": 2955,
      "key": "fadef9ce-0f28-4792-bb3f-6d0bd5c6a055",
      "status": "created",
      "created_at": "2022-10-27T09:44:50.800-03:00",
      "updated_at": "2022-10-27T09:46:45.968-03:00",
      "file": null
    }
  }
}
```

Esse endpoint obtem todos os dados de uma proposta

### HTTP Request

`GET https://app.securities.com.br/api/v1/proposals/:id`

## Criar proposta

> Request:

```shell
curl -X POST https://app.securities.com.br/api/v1/proposals \
   -H "Authorization: Bearer $TOKEN" \
   -H "Content-Type: application/json" \
   -d '{
        "proposal": {
          "number": "1234567",
          "issuer_full_name": "Hugo Fonseca",
          "issuer_document": "525.403.396-61",
          "installments": 48,
          "template_key": "e7c3534c-2b04-11ed-a261-02422b00ac13",
          "document_data": {
            "number": 231387,
            "issuer_full_name": "Hugo Fonseca",
            "issuer_full_address": "Setor M QNM 03 Conjunto Z - 72200-000, Brasília - DF",
            "issuer_cpf": "657.565.000-73",
            "issuer_rg": "47.825.277-8",
            "issuer_cnh": "81457959115",
            "issuer_email": "hugo@email.com",
            "guarantor_full_name": "Juan Isaac Fogaça",
            "guarantor_cpf": "822.448.901-98",
            "guarantor_rg": "34.576.797-4",
            "guarantor_full_address": "Quadra Quadra 300 Conjunto 31 - 72260-132, Brasília - DF",
            "financed_amount": 125314.12,
            "bank_name": "341 - Banco Itaú",
            "bank_agency_number": 7957,
            "bank_account_number": 423762,
            "disbursed_amount": 108323.45,
            "tac": 42.89,
            "pmt": 2784.12,
            "maturity": 60,
            "ccb_registration_fee": 88.32,
            "first_installment_due_date": "31/10/2022",
            "last_installment_due_date": "31/10/2027",
            "iof": 43.21,
            "commercial_yearly_interest_rate": 13.42,
            "commercial_monthly_interest_rate": 2.21,
            "cet_yearly_rate": 21.32,
            "cet_monthly_rate": 9.87
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
    "id": 3073,
    "number": "123321",
    "issuer_full_name": "Hugo Fonseca",
    "issuer_document": "882.793.334-44",
    "installments": 48,
    "created_at": "2022-10-27T09:44:50.772-03:00",
    "updated_at": "2022-10-27T09:44:50.772-03:00",
    "document_data": {
      "number": 231387,
      "issuer_full_name": "Hugo Fonseca",
      "issuer_full_address": "Setor M QNM 03 Conjunto Z - 72200-000, Brasília - DF",
      "issuer_cpf": "657.565.000-73",
      "issuer_rg": "47.825.277-8",
      "issuer_cnh": "81457959115",
      "issuer_email": "hugo@email.com",
      "guarantor_full_name": "Juan Isaac Fogaça",
      "guarantor_cpf": "822.448.901-98",
      "guarantor_rg": "34.576.797-4",
      "guarantor_full_address": "Quadra Quadra 300 Conjunto 31 - 72260-132, Brasília - DF",
      "financed_amount": 125314.12,
      "bank_name": "341 - Banco Itaú",
      "bank_agency_number": 7957,
      "bank_account_number": 423762,
      "disbursed_amount": 108323.45,
      "tac": 42.89,
      "pmt": 2784.12,
      "maturity": 60,
      "ccb_registration_fee": 88.32,
      "first_installment_due_date": "31/10/2022",
      "last_installment_due_date": "31/10/2027",
      "iof": 43.21,
      "commercial_yearly_interest_rate": 13.42,
      "commercial_monthly_interest_rate": 2.21,
      "cet_yearly_rate": 21.32,
      "cet_monthly_rate": 9.87
    },
    "document": {
      "id": 2955,
      "key": "fadef9ce-0f28-4792-bb3f-6d0bd5c6a055",
      "status": "created",
      "created_at": "2022-10-27T09:44:50.800-03:00",
      "updated_at": "2022-10-27T09:46:45.968-03:00",
      "file": null
    }
  }
}
```

Esse endpoint cria uma proposta

### HTTP Request

`POST https://app.securities.com.br/api/v1/proposals`

### Parâmetros da requisição

| Parâmetro       | Obrigatório | Tipo    | Descrição                               |
| --------------- | ----------- | ------- | --------------------------------------- |
| number          | sim         | string  | Número da proposta                      |
| issuer_document | sim         | string  | Documento do emitente                   |
| installments    | sim         | integer | Quantidade de parcelas                  |
| template_key    | sim         | string  | Chave do template no assinador          |
| document_data   | sim         | json    | Dados do documento para compor o título |
