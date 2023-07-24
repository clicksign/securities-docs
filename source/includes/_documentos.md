# Documentos

Recursos utilizados para gerenciar arquivos em PDF.

## Obter um documento pela key

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/documents/bykey/:key \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
    "document": {
        "id": 394193,
        "key": "0aa3e5bc-3a88-4873-b680-8ec7ecea585e",
        "status": "validated",
        "created_at": "2023-07-24T10:53:54.295-03:00",
        "updated_at": "2023-07-24T11:02:44.586-03:00",
        "file": {
            "url": "https://securities-app.s3.amazonaws.com/"
        }
    }
}
```

Esse endpoint obtêm um documento e pela key.

### HTTP Request

`GET https://app.securities.com.br/api/v1/documents/bykey/:key`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| key      | uuid | Chave do documento |
