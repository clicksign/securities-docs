# API Nova Securities

## Registro de CCBs

### Proposta

A proposta é o documento que representa a CCB antes dela ser assinada pelo tomador. Enquanto o tomador não assina o documento, ele ainda não se tornou uma CCB para ser cedida, então esse documento é uma Proposta de se tornar uma CCB.

A proposta conterá todos os dados de uma CCB, seguindo o modelo preconizado entre originador e fundo, entretanto, o que o diferencia de uma CCB é o fato de ainda não estar assinado pelo tomador.

#### Listar propostas

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
      "updated_at": "2022-10-07T12:00:33.571-03:00",
      "url": "https://app.securities.com.br/api/v1/proposals/218"
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

`GET https://app.securities.com.br/api/v1/proposals`

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| page      | integer | Paginação |

#### Obter proposta

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
    "documents": [
      {
        "id": 2955,
        "key": "fadef9ce-0f28-4792-bb3f-6d0bd5c6a055",
        "status": "created",
        "created_at": "2022-10-27T09:44:50.800-03:00",
        "updated_at": "2022-10-27T09:46:45.968-03:00",
        "file": null
      }
    ],
    "url": "https://app.securities.com.br/api/v1/proposals/3073"
  }
}
```

Esse endpoint obtem todos os dados de uma proposta

`GET https://app.securities.com.br/api/v1/proposals/:id`

#### Criar proposta

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
    "documents": [
      {
        "id": 2955,
        "key": "fadef9ce-0f28-4792-bb3f-6d0bd5c6a055",
        "status": "created",
        "created_at": "2022-10-27T09:44:50.800-03:00",
        "updated_at": "2022-10-27T09:46:45.968-03:00",
        "file": null
      }
    ],
    "url": "https://app.securities.com.br/api/v1/proposals/3073"
  }
}
```

Esse endpoint cria uma proposta

`POST https://app.securities.com.br/api/v1/proposals`

| Parâmetro       | Obrigatório | Tipo    | Descrição                               |
| --------------- | ----------- | ------- | --------------------------------------- |
| number          | sim         | string  | Número da proposta                      |
| issuer_full_name| sim         | string  | Nome completo do emitente               |
| issuer_document | sim         | string  | Documento do emitente                   |
| installments    | sim         | integer | Quantidade de parcelas                  |
| template_key    | sim         | string  | Chave do template no assinador          |
| document_data   | sim         | json    | Dados do documento para compor o título |

### Signatário

Os signatários são aqueles que irão assinar os documentos envolvidos no processo de securitização, desde o registro de uma proposta, sendo o signatário o tomador, até a cessão de uma ou mais CCBs num lote, sendo assinadas pelo originador do crédito e fundo de investimento, como signatários.

#### Listar signatários

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/signers \
     -H "Authorization: Bearer $TOKEN"
```

```shell
curl -X GET https://app.securities.com.br/api/v1/documents/:document_id/signers \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "signers": [
    {
      "id": 3,
      "full_name": "John Carter",
      "has_documentation": false,
      "documentation": null,
      "email": "signer@example.com",
      "birthday": "1987-09-09",
      "phone_number": "(16) 98234-3045",
      "auth": "email",
      "communicate_by": "email",
      "key": "690e1c32-7edd-48e4-b083-a738f05b4d7e",
      "sign_as": "sign",
      "selfie_enabled": false,
      "official_document_enabled": false,
      "liveness_enabled": false,
      "handwritten_enabled": false,
      "facial_biometrics_enabled": false,
      "created_at": "2022-09-08T15:37:05.189-03:00",
      "updated_at": "2022-09-15T15:26:18.880-03:00",
      "url": "https://app.securities.com.br/api/v1/signers/3" 
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

Esse endpoint lista todos os signatários

Todos os signatários

`GET https://app.securities.com.br/api/v1/signers`

<br>Signatários por documento

`GET https://app.securities.com.br/api/v1/documents/:document_id/signers`

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| page      | integer | Paginação |

#### Obter signatário

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/documents/:document_id/signers/:id \
     -H "Authorization: Bearer $TOKEN"
```

```shell
curl -X GET https://app.securities.com.br/api/v1/signers/:id \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "signer": {
    "id": 1,
    "full_name": "John Carter",
    "has_documentation": false,
    "documentation": null,
    "email": "signer@example.com",
    "birthday": "1987-09-09",
    "phone_number": "(16) 98234-3045",
    "auth": "email",
    "communicate_by": "email",
    "key": "690e1c32-7edd-48e4-b083-a738f05b4d7e",
    "sign_as": "sign",
    "selfie_enabled": false,
    "official_document_enabled": false,
    "liveness_enabled": false,
    "handwritten_enabled": false,
    "facial_biometrics_enabled": false,
    "created_at": "2022-09-08T15:37:05.189-03:00",
    "updated_at": "2022-09-15T15:26:18.880-03:00"
  }
}
```

Esse endpoint obtém todos os dados de um signatário. É possível obter o signatário pelo `:id` ou pela `:key`

Obter signatário

`GET https://app.securities.com.br/api/v1/signers/:id`<br>
`GET https://app.securities.com.br/api/v1/signers/bykey/:key`

<br>Obter signatário de um documento

`GET https://app.securities.com.br/api/v1/documents/:document_id/signers/:id`<br>
`GET https://app.securities.com.br/api/v1/documents/:document_id/signers/bykey/:key`

#### Criar signatário

> Request:

```shell
curl -X POST https://app.securities.com.br/api/v1/documents/:document_id/signers \
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
            "communicate_by": "email"
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
    "selfie_enabled": false,
    "official_document_enabled": false,
    "liveness_enabled": false,
    "handwritten_enabled": false,
    "facial_biometrics_enabled": false,
    "created_at": "2022-09-16T18:41:00.079-03:00",
    "updated_at": "2022-09-16T18:41:00.079-03:00"
  }
}
```

Esse endpoint cria um signatário

Criar signatário avulso

`POST https://app.securities.com.br/api/v1/signers`

<br>Criar signatário vinculado a um documento

`POST https://app.securities.com.br/api/v1/documents/:document_id/signers`

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
    "selfie_enabled": false,
    "official_document_enabled": false,
    "liveness_enabled": false,
    "handwritten_enabled": false,
    "facial_biometrics_enabled": false,
    "created_at": "2022-09-16T18:41:00.079-03:00",
    "updated_at": "2022-09-16T18:41:00.079-03:00"
  },
  "lists": [
    {
      "id": 113,
      "signer_id": 4,
      "document_id": 43,
      "key": "2dd1f865-2154-4f7c-8b3b-9bcbcbcbac9b",
      "batch_key": "14fb4ce9-f28e-4954-a884-ad125931181b",
      "request_signature_key": "c1243577-73f5-4071-9ba4-59d5a2f13ee7",
      "signed": false,
      "sign_as": "sign",
      "created_at": "2022-10-26T15:53:18.825-03:00",
      "updated_at": "2022-10-26T15:55:51.010-03:00",
      "url": "https://app.securities.com.br/api/v1/lists/113"
    }
  ]
}
```

| Parâmetro         | Obrigatório | Tipo    | Descrição                                                     |
| ----------------- | ----------- | ------- | ------------------------------------------------------------- |
| full_name         | sim         | string  | Nome completo                                                 |
| has_documentation | não         | boolean (default true) | Tem documentação, como CPF, CNPJ ou Passaporte.               |
| documentation     | condicional | string  | CPF, CNPJ ou Passaporte                                       |
| birthday          | condicional | string  | Data de nascimento                                            |
| email             | condicional | string  | E-mail                                                        |
| phone_number      | sim         | string  | Número de telefone                                            |
| auth              | sim         | string  | Tipo de autenticação: "email", "api" ou "tokenless"           |
| communicate_by    | sim         | string  | Por onde será notificado: "email"                             |
| sign_as           | sim         | string  | Assinar como: sign, party, witness, contractor, contractee... |
| selfie_enabled    | não         | boolean (default false)  | Assinar como: sign, party, witness, contractor, contractee... |
| handwritten_enabled       | não         | boolean (default false)  | Define a solicitação de assinatura manuscrita como ponto de autenticação para o signatário. |
| official_document_enabled | não         | boolean (default false)  | Define a solicitação da foto (frente e verso) do documento oficial como ponto de autenticação para o signatário. |
| liveness_enabled          | não         | boolean (default false)  | Define a solicitação de selfie dinâmica como ponto de autenticação para o signatário. |
| facial_biometrics_enabled | não         | boolean (default false)  | Define a solicitação de biometria facial como ponto de autenticação para o signatário. |

### CCB

CCB é a Cédula de crédito bancário: A Cédula de Crédito Bancário é título de crédito emitido por emissor-devedor em favor de instituição financeira, representando promessa de pagamento em dinheiro, decorrente de operação de crédito, de qualquer modalidade. Sobre a regulação da CCB, vide o art. 26 da Lei 10.931/2004.

Em outras palavras, a CCB é o que representará um crédito tomado e que foi assinado pelo tomador para que possa ser negociado como um título no mercado financeiro.

#### ATENCÃO

Foram atualizadas as rotas das CCBs:

Antes: `/api/v1/securities`

Agora: `/api/v1/bank_credit_notes`

#### Listar CCBs

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/bank_credit_notes \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "bank_credit_notes": [
    {
      "id": 2,
      "number": "123456",
      "issuer_full_name": "Hugo Fonseca",
      "issuer_document": "630.427.604-48",
      "installments": 1,
      "created_at": "2022-09-15T15:27:00.691-03:00",
      "updated_at": "2022-09-15T15:27:00.691-03:00",
      "url": "https://app.securities.com.br/api/v1/bank_credit_notes/2"
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

Esse endpoint lista todas as CCBs

`GET https://app.securities.com.br/api/v1/bank_credit_notes`

| Parâmetro | Tipo    | Descrição     |
| --------- | ------- | ------------- |
| number    | string  | Número da CCB |
| page      | integer | Paginação     |

#### Obter CCB

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/bank_credit_notes/:number \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "bank_credit_note": {
    "id": 2,
    "number": "123456",
    "issuer_full_name": "Hugo Fonseca",
    "issuer_document": "630.427.604-48",
    "installments": 1,
    "signature_provider": "clicksign",
    "created_at": "2022-09-15T15:27:00.691-03:00",
    "updated_at": "2022-09-15T15:27:00.691-03:00",
    "documents": [
      {
        "id": 23,
        "key": "fadef9ce-0f28-4792-bb3f-6d0bd5c6a055",
        "status": "created",
        "created_at": "2022-10-27T09:44:50.800-03:00",
        "updated_at": "2022-10-27T09:46:45.968-03:00",
        "file": null
      }
    ],
    "url": "https://app.securities.com.br/api/v1/bank_credit_notes/123456"
  }
}
```

Esse endpoint obtém todos os dados de uma CCB

`GET https://app.securities.com.br/api/v1/bank_credit_notes/:number`

#### Criar CCB já assinada para Cessão

> Request:

```shell
curl -v POST https://app.securities.com.br/api/v1/bank_credit_notes \
     -H "Authorization: Bearer $TOKEN"
     -F "file=@file1.pdf"
     -F "signed=true"
     -F "signature_provider=govbr"
     -F "number=37891673"
     -F "installments=12"
     -F "issuer_full_name=Hugo Fonseca"
     -F "issuer_document=04218776143"
     -F "document_data={\"car\": \"Volkswagen\"}"

```

> Response:

```shell
HTTP/1.1 201 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "bank_credit_note": {
    "id": 2,
    "number": "123456",
    "issuer_full_name": "Hugo Fonseca",
    "issuer_document": "630.427.604-48",
    "installments": 1,
    "signature_provider": "clicksign",
    "created_at": "2022-09-15T15:27:00.691-03:00",
    "updated_at": "2022-09-15T15:27:00.691-03:00",
    "documents": [
      {
        "id": 23,
        "key": "fadef9ce-0f28-4792-bb3f-6d0bd5c6a055",
        "status": "validated",
        "created_at": "2022-10-27T09:44:50.800-03:00",
        "updated_at": "2022-10-27T09:46:45.968-03:00",
        "file": {
          "url": "https://example.com/path/to/document.pdf"
        }
      }
    ],
    "url": "https://app.securities.com.br/api/v1/bank_credit_notes/2"
  }
}
```

Endpoint que recebe títulos CCBs já assinados pelo tomador fora dos produtos Clicksign, mas que serão cedidos na Clicksign Securities.

<aside class="notice">
Este endpoint tem como funcionalidade a recepção de CCBs que serão endossadas e cedidas pela Clicksign Securities, porém, o seu registro não ocorreu nos produtos Clicksign, ou seja, receberemos aqui uma CCB (.pdf) previamente registrada e assinada por produtos terceiros.

Caso o objetivo seja de criar uma CCB, registrando-a na Clicksign Securities para então também ser cedida com nossos produtos, agora ou no momento oportuno de movimentação do estoque de títulos, consulte nossa API de Proposta (título antes de se tornar uma CCB assinada pelo tomador).
</aside>

`POST https://app.securities.com.br/api/v1/bank_credit_notes`

Essa requisição deve ser um `multipart/form-data` com os seguintes parâmetros:

| Parâmetro             | Tipo    | Descrição                                                                       |
| --------------------- | --------| ------------------------------------------------------------------------------- |
| file                  | File    | Upload do pdf que será anexado a CCB                                            |
| signed                | boolean | Boolean indicando se o pdf fornecido está assinado                              |
| signature_provider    | string  | String indicando qual assinador foi utilizado. Ver assinadores aceitos abaixo.  |
| number                | string  | Número da CCB                                                                   |
| issuer_full_name      | string  | Nome completo do emitente                                                       |
| issuer_document       | string  | Documento do emitente                                                           |
| installments          | integer | Número de parcelas                                                              |
| document_data         | string  | Serialização do json com os dados do documento para compor a CCB                |

- Lista de assinadores suportados no momento:

| Parâmetro (utilizar na request) | Nome de exibição    |
| ------------------------------- | --------------------|
|d4sign | D4Sign |
|zapsign | ZapSign |
|docusign | Docusign |
|totvs | Assinatura eletrônica TOTVS |
|autentique | Autentique |
|assinebem | Assine Bem |
|contraktor | Contraktor |
|juridoc | Juridoc |
|santocontrato | Santo Contrato |
|certisign | Certisign |
|signnow | SignNow |
|adobesign | Adobe Sign |
|hellosign | Hello Sign |
|webdox | Webdox |
|sdocsafe | Sdoc Safe |
|accesscorp | Access Corp |
|ebox | eBox Digital |
|arquivar | Arquivar |
|unico | Unico |
|formalizar | Formalizar e-Signature |
|onedoc | 1Doc |
|bry | Bry |
|quicksoft | QuickSoft |
|fepweb | FepWeb |
|govbr | Gov.br |
|flexdoc | Flexdoc |
|brysigner | Bry Signer |
|besign | Besign |
|letssign | LetsSign |
|assertiva | Assertiva |
|optime | Optime |
|digicert | Digicert |
|qcertifica | Q Certifica |
|fast4sign | Fast4Sign |

## Cessão de títulos
