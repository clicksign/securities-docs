# Signatário do documento

**TODO:** Signatários do documento...

## Listar signatários do documento

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/lists \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "lists": [
    {
      "id": 113,
      "signer_id": 18,
      "document_id": 43,
      "key": "2dd1f865-2154-4f7c-8b3b-9bcbcbcbac9b",
      "batch_key": "14fb4ce9-f28e-4954-a884-ad125931181b",
      "request_signature_key": "c1243577-73f5-4071-9ba4-59d5a2f13ee7",
      "signed": false,
      "sign_as": "sign",
      "created_at": "2022-10-26T15:53:18.825-03:00",
      "updated_at": "2022-10-26T15:55:51.010-03:00"
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

Esse endpoint lista todos signatários de um documento e vice-versa

### HTTP Request

`GET https://app.securities.com.br/api/v1/lists`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| page      | integer | Paginação |

## Obter signatário do documento

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/lists/:id \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "list": {
    "id": 113,
    "signer_id": 18,
    "document_id": 43,
    "key": "2dd1f865-2154-4f7c-8b3b-9bcbcbcbac9b",
    "batch_key": "14fb4ce9-f28e-4954-a884-ad125931181b",
    "request_signature_key": "c1243577-73f5-4071-9ba4-59d5a2f13ee7",
    "signed": false,
    "sign_as": "sign",
    "created_at": "2022-10-26T15:53:18.825-03:00",
    "updated_at": "2022-10-26T15:55:51.010-03:00"
  }
}
```

Esse endpoint obtém todos signatários de um documento e vice-versa

### HTTP Request

`GET https://app.securities.com.br/api/v1/lists/:id`

## Adicionar signatários no documento

> Request:

```shell
curl -X POST https://app.securities.com.br/api/v1/lists \
     -H "Authorization: Bearer $TOKEN" \
     -H "Content-Type: application/json" \
     -d '{
          "list": {
            "signer_id": 1,
            "document_id": 2,
            "sign_as": "sign"
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
    "id": 113,
    "signer_id": 18,
    "document_id": 43,
    "key": "2dd1f865-2154-4f7c-8b3b-9bcbcbcbac9b",
    "batch_key": "14fb4ce9-f28e-4954-a884-ad125931181b",
    "request_signature_key": "c1243577-73f5-4071-9ba4-59d5a2f13ee7",
    "sign_as": "sign",
    "created_at": "2022-10-26T15:53:18.825-03:00",
    "updated_at": "2022-10-26T15:55:51.010-03:00"
  }
}
```

Esse endpoint associa o signatário a um documento e vice-versa

### HTTP Request

`POST https://app.securities.com.br/api/v1/lists`

### Parâmetros da requisição

| Parâmetro   | Obrigatório | Tipo    | Descrição                                                  |
| ----------- | ----------- | ------- | ---------------------------------------------------------- |
| signer_id   | sim         | integer | ID do signatário                                           |
| document_id | sim         | string  | ID do documento                                            |
| sign_as     | não         | string  | Assinar como: sign (padrão), party, witness, contractor... |
