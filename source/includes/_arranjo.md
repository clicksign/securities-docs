# Arranjo

**TODO:** O Arranjo é utilizada para....

## Listar Arranjos

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/arrangements \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "arrangements": [
    {
      "id": 1,
      "account_id": 1,
      "member_id": 2,
      "member_type": "endorser"
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

Esse endpoint lista todos os Arranjos

### HTTP Request

`GET https://app.securities.com.br/api/v1/arrangements`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| page      | integer | Paginação |

## Obter Arranjo

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/arrangements/:id \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "arrangement": {
    "id": 1,
    "account_id": 1,
    "member_id": 2,
    "member_type": "endorser",
    "signers": [
      {
        "id": 100,
        "account_id": 218,
        "document_type": "Proposal",
        "document_id": 99,
        "full_name": "Latia Pouros Roberts",
        "has_documentation": true,
        "documentation": "062.231.968-06",
        "email": "rufus@quitzon.co",
        "birthday": "1964-10-22",
        "phone_number": "(52) 91647-1229",
        "auth": "email",
        "communicate_by": "email",
        "created_at": "2022-09-29T14:18:21.007-03:00",
        "updated_at": "2022-09-29T14:18:21.007-03:00",
        "key": "9429903a-ba8d-4eca-be62-d5d034bd0f52",
        "sign_as": "sign",
        "link_key": "f122bf00-f6d8-4567-b305-d7163f4fda89",
        "batch_key": "3b751793-59b2-40a0-b421-758632ce28fe"
      },
      ...
    ]
  }
}
```

Esse endpoint obtem todos os dados de um Arranjo

### HTTP Request

`GET https://app.securities.com.br/api/v1/arrangements/:id`
