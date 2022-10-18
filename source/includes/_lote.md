# Lote

**TODO:** O lote é utilizado para....

## Listar lotes

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/batches \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
[
  {
    "id": 1,
    "status": "pending",
    "number": "123",
    "quantity": 1,
    "created_at": "2022-10-06T16:46:40.705-03:00",
    "updated_at": "2022-10-06T16:46:40.889-03:00"
  }
]
```

Esse endpoint lista todos os lotes

### HTTP Request

`GET https://app.securities.com.br/api/v1/batches`

## Obter um lote

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/batches/:id \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "id": 1,
  "status": "pending",
  "number": "123",
  "quantity": 1,
  "created_at": "2022-10-06T16:46:40.705-03:00",
  "updated_at": "2022-10-06T16:46:40.889-03:00"
}
```

Esse endpoint obtem todos os dados de um lote

### HTTP Request

`GET https://app.securities.com.br/api/v1/batches/:id`

## Criar lote

> Request:

```shell
curl -X POST https://app.securities.com.br/api/v1/batches \
     -H "Authorization: Bearer $TOKEN" \
     -H "Content-Type: application/json" \
     -d '{
          "batch": {
            "number": "123",
            "quantity": 1,
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
  "id": 1,
  "status": "pending",
  "number": "123",
  "quantity": 1,
  "created_at": "2022-10-06T16:46:40.705-03:00",
  "updated_at": "2022-10-06T16:46:40.889-03:00"
}
```

Esse endpoint cria um lote

### HTTP Request

`POST https://app.securities.com.br/api/v1/batches`

### Parâmetros da requisição

| Parâmetro | Obrigatório | Tipo    | Descrição                     |
| --------- | ----------- | ------- | ----------------------------- |
| quantity  | sim         | integer | Quantidade de títulos no lote |
| number    | sim         | integer | Número do lote                |

### Validações

Enquanto `quantity` não for equivalente a quantidade total de títulos do lote, o processamento não será finalizado,
o status iniciará em `pending`, irá para `checking` após adicionar o primeiro título no lote e, até que todos os
títulos sejam enviados, permanecerá nesse status.

Não será permitido enviar uma quantidade de títulos maior que `quantity`.
