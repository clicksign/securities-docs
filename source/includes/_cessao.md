# Termos de Cessão

**TODO:** O contrato de cessão é utilizado para....

## Listar termos de cessão

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/assignments \
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
    "assignee_id": 1,
    "endorser_id": 1,
    "batch_id": 3,
    "number": "123456",
    "issue_date": "2022-09-30",
    "status": "pending",
    "full_amount": "100.0",
    "created_at": "2022-09-30T18:13:53.140-03:00",
    "updated_at": "2022-09-30T18:13:53.175-03:00"
  }
]
```

Esse endpoint lista todos os termos de cessão

### HTTP Request

`GET https://app.securities.com.br/api/v1/assignments`

## Obter contrato de cessão

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/assignments/:id \
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
  "assignee_id": 1,
  "endorser_id": 1,
  "batch_id": 3,
  "number": "123456",
  "issue_date": "2022-09-30",
  "status": "pending",
  "full_amount": "100.0",
  "created_at": "2022-09-30T18:13:53.140-03:00",
  "updated_at": "2022-09-30T18:13:53.175-03:00"
}
```

Esse endpoint obtem todos os dados de um termo de cessão

### HTTP Request

`GET https://app.securities.com.br/api/v1/assignments/:id`

## Criar termo de cessão

> Request:

```shell
curl -X POST https://app.securities.com.br/api/v1/assignments \
     -H "Authorization: Bearer $TOKEN" \
     -H "Content-Type: application/json" \
     -d '{
          "assignment": {
            "assignee_id": 1,
            "endorser_id": 1,
            "number": "123456",
            "issue_date": "2022-09-30",
            "full_amount": 100.0,
            "batch_id": 3
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
  "assignee_id": 1,
  "endorser_id": 1,
  "batch_id": 3,
  "number": "123456",
  "issue_date": "2022-09-30",
  "status": "pending",
  "full_amount": "100.0",
  "created_at": "2022-09-30T18:13:53.140-03:00",
  "updated_at": "2022-09-30T18:13:53.175-03:00"
}
```

Esse endpoint cria um termo de cessão

### HTTP Request

`POST https://app.securities.com.br/api/v1/assignments`

### Parâmetros da requisição

Parâmetro                | Obrigatório | Tipo     | Descrição
------------------       | ----------- | -------- | -----------
assignee_id              | sim         | integer  | ID da conta da cessionária
endorser_id              | sim         | integer  | ID da conta do endossatário
number                   | sim         | string   | Número do termo de cessão
issue_date               | sim         | boolean  | Data de emissão
full_amount              | sim         | float    | Valor do termo (soma de todos os títulos)
batch_id                 | sim         | integer  | ID do Lote de CCBs

### Validações

O valor inserido em `full_amount` não é validado, ou seja, se inserir um valor diferente da soma dos valores dos títulos
poderá ter divergências. O motivo da não validação é porque o valor negociado pode ser menor que o valor da soma dos títulos,
sendo assim, não há com que comparar os valores inseridos, sendo esperado, em alguns casos, alguma divergência.

