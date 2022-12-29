# CCB

CCB é a Cédula de crédito bancário: A Cédula de Crédito Bancário é título de crédito emitido por emissor-devedor em favor de instituição financeira, representando promessa de pagamento em dinheiro, decorrente de operação de crédito, de qualquer modalidade. Sobre a regulação da CCB, vide o art. 26 da Lei 10.931/2004.

Em outras palavras, a CCB é o que representará um crédito tomado e que foi assinado pelo tomador para que possa ser negociado como um título no mercado financeiro.

## Listar CCBs

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/securities \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "securities": [
    {
      "id": 2,
      "number": "123456",
      "issuer_full_name": "Hugo Fonseca",
      "issuer_document": "630.427.604-48",
      "installments": 1,
      "created_at": "2022-09-15T15:27:00.691-03:00",
      "updated_at": "2022-09-15T15:27:00.691-03:00"
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

### HTTP Request

`GET https://app.securities.com.br/api/v1/securities`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição     |
| --------- | ------- | ------------- |
| number    | string  | Número da CCB |
| page      | integer | Paginação     |

## Obter CCB

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/securities/:id \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "security": {
    "id": 2,
    "number": "123456",
    "issuer_full_name": "Hugo Fonseca",
    "issuer_document": "630.427.604-48",
    "installments": 1,
    "document_data": {
      "event": {
        "data": null,
        "name": "auto_close",
        "occurred_at": "2022-09-15T15:27:00.361-03:00"
      },
      "document": {
        "key": "e646a204-6e57-4e94-b799-fca7f1002c6a",
        "path": "/Proposals/Proposta 123456.docx",
        "events": [
          ...
        ]
      }
    },
    "created_at": "2022-09-15T15:27:00.691-03:00",
    "updated_at": "2022-09-15T15:27:00.691-03:00",
  }
}
```

Esse endpoint obtem todos os dados de uma CCB

### HTTP Request

`GET https://app.securities.com.br/api/v1/securities/:id`
