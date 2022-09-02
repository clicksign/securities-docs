# Proposta

A proposta é utilizada para....


## Criar proposta

> Request:

```shell
curl -X POST https://api.securities.com.br/v1/proposals
   -H 'Authorization: Bearer <ACCESS_TOKEN>'
   -d '{
        "number": "1234567",
        "issuer_document": "525.403.396-61",
        "installments": 48,
        "document_key": "534e7c3c-2b04-11ed-a261-0242ac120002",
        "metadata": {
          "bank_account_number": "32938-1",
          "bank_agency_number": "2384",
          "bank_name": "Itau",
          ...
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
  "number": "1234567",
  "issuer_document": "525.403.396-61",
  "installments": 48,
  "document_key": "534e7c3c-2b04-11ed-a261-0242ac120002",
  "metadata": {
    "bank_account_number": "32938-1",
    "bank_agency_number": "2384",
    "bank_name": "Itau",
    ...
  }
}
```

Esse endpoint cria uma proposta

### HTTP Request

`POST https://api.securities.com.br/v1/proposals`

### Parâmetros da requisição

Parâmetro        | Obrigatório | Tipo        | Descrição
---------------- | ----------- | ----------- | -----------
number           | sim         | string      | Número da proposta
issuer_document  | sim         | string      | Documento do emitente
installments     | sim         | integer     | Quantidade de parcelas
document_key     | sim         | sim         | Chave do documento no assinador
metadata         | sim         | json        | Metadados com informações para compor o título
