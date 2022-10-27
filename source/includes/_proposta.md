# Proposta

**TODO:** A proposta é utilizada para....

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
    "issuer_document": "882.793.334-44",
    "installments": 48,
    "created_at": "2022-10-27T09:44:50.772-03:00",
    "updated_at": "2022-10-27T09:44:50.772-03:00",
    "document_data": {
      "bank_account_number": "32938-1",
      "bank_agency_number": "2384",
      "bank_name": "Itau",
      ...
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
          "issuer_document": "525.403.396-61",
          "installments": 48,
          "template_key": "e7c3534c-2b04-11ed-a261-02422b00ac13",
          "document_data": {
            "bank_account_number": "32938-1",
            "bank_agency_number": "2384",
            "bank_name": "Itau",
            ...
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
    "issuer_document": "882.793.334-44",
    "installments": 48,
    "created_at": "2022-10-27T09:44:50.772-03:00",
    "updated_at": "2022-10-27T09:44:50.772-03:00",
    "document_data": {
      "bank_account_number": "32938-1",
      "bank_agency_number": "2384",
      "bank_name": "Itau",
      ...
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
