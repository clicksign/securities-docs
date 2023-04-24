# Lote

O Lote de cessão é o conjunto de CCBs que estão agrupadas para a mesma finalidade: Serem cedidas numa negociação entre cedente e cessionário.

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
{
  "batches": [
    {
      "id": 1,
      "status": "pending",
      "number": "123",
      "quantity": 1,
      "quantity_added": 1,
      "quantity_approved": 1,
      "quantity_signed": 1,
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

Esse endpoint lista todos os lotes

### HTTP Request

`GET https://app.securities.com.br/api/v1/batches`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| page      | integer | Paginação |

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
  "batch": {
    "id": 1,
    "status": "pending",
    "number": "123",
    "quantity": 1,
    "quantity_added": 1,
    "quantity_approved": 1,
    "quantity_signed": 1,
    "created_at": "2022-10-06T16:46:40.705-03:00",
    "updated_at": "2022-10-06T16:46:40.889-03:00"
  }
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
            "quantity": 1
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
  "batch": {
    "id": 1,
    "status": "pending",
    "number": "123",
    "quantity": 1,
    "quantity_added": 0,
    "quantity_approved": 0,
    "quantity_signed": 0,
    "created_at": "2022-10-06T16:46:40.705-03:00",
    "updated_at": "2022-10-06T16:46:40.889-03:00"
  }
}
```

Esse endpoint cria um lote

### HTTP Request

`POST https://app.securities.com.br/api/v1/batches`

### Parâmetros da requisição

| Parâmetro | Obrigatório | Tipo    | Descrição                     |
| --------- | ----------- | ------- | ----------------------------- |
| quantity  | sim         | integer | Quantidade de títulos no lote |
| number    | sim         | string  | Número do lote                |

### Validações

Enquanto `quantity` não for equivalente a quantidade total de títulos do lote, o processamento não será finalizado,
o status iniciará em `pending`, irá para `checking` após adicionar o primeiro título no lote e, até que todos os
títulos sejam enviados, permanecerá nesse status.

<aside class="warning">
  Não será permitido enviar uma quantidade de títulos maior que <code>batch.quantity</code>.
</aside>
