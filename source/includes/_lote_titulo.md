# Título em Lote

**TODO:** O título no lote é utilizado para....

## Listar títulos do lote

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/batches/:batch_id/security_batches \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "security_batches": [
    {
      "id": 1,
      "security_id": 1,
      "batch_id": 1,
      "status": "pending",
      "created_at": "2022-10-06T16:46:40.705-03:00",
      "updated_at": "2022-10-06T16:46:40.889-03:00"
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

Esse endpoint lista todos os títulos do lote

### HTTP Request

`GET https://app.securities.com.br/api/v1/batches/:batch_id/security_batches`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| page      | integer | Paginação |

## Obter um título do lote

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/batches/:batch_id/security_batches/:id \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "security_batch": {
    "id": 1,
    "security_id": 1,
    "batch_id": 1,
    "status": "pending",
    "created_at": "2022-10-06T16:46:40.705-03:00",
    "updated_at": "2022-10-06T16:46:40.889-03:00"
  }
}
```

Esse endpoint obtem todos os dados de um título de um lote

### HTTP Request

`GET https://app.securities.com.br/api/v1/batches/:batch_id/security_batches/:id`

## Adicionar título no lote

> Request:

```shell
curl -X POST https://app.securities.com.br/api/v1/batches/:batch_id/security_batches \
     -H "Authorization: Bearer $TOKEN" \
     -H "Content-Type: application/json" \
     -d '{
          "security_batch": {
            "security_id": 1
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
  "security_batch": {
    "id": 1,
    "security_id": 1,
    "batch_id": 1,
    "status": "pending",
    "created_at": "2022-10-06T16:46:40.705-03:00",
    "updated_at": "2022-10-06T16:46:40.889-03:00"
  }
}
```

Esse endpoint adiciona um título no lote

### HTTP Request

`POST https://app.securities.com.br/api/v1/batches/:batch_id/security_batches`

### Parâmetros da requisição

| Parâmetro   | Obrigatório | Tipo    | Descrição    |
| ----------- | ----------- | ------- | ------------ |
| security_id | sim         | integer | ID do título |

### Validações

Enquanto `quantity` não for equivalente a quantidade total de títulos do lote, o processamento não será finalizado,
o status iniciará em `pending`, irá para `checking` após adicionar o primeiro título no lote e, até que todos os
títulos sejam enviados, permanecerá nesse status.

Não será permitido enviar uma quantidade de títulos maior que `quantity`.

<aside class="warning">
  <strong>Atenção</strong><br>
  Para obter o <code>security_id</code> será necessário <a href="#listar-titulos">consultar pelo título</a> no respectivo endpoint.
</aside>
