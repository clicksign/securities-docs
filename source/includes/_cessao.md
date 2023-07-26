# Termos de Cessão

O termo de cessão é o instrumento através do qual se opera a transmissão de direitos sobre determinado bem. Por meio dela, o vendedor, conhecido como cedente, repassa ao comprador, denominado cessionário, os direitos sobre o bem objeto da Cessão.

O termo de cessão é o documento que transcreve de forma resumida a operação que está sendo cedida naquele momento, com o resumo das CCBs que estão em operação no lote.

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
    "arrangement_id": 1,
    "batch_id": 3,
    "number": "123456",
    "issue_date": "2022-09-30",
    "status": "pending",
    "full_amount": "100.0",
    "operation_type": "duplicate",
    "created_at": "2022-09-30T18:13:53.140-03:00",
    "updated_at": "2022-09-30T18:13:53.175-03:00",
    "url": "https://app.securities.com.br/api/v1/assignments/1"
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
  "arrangement_id": 1,
  "batch_id": 3,
  "number": "123456",
  "issue_date": "2022-09-30",
  "status": "pending",
  "full_amount": "100.0",
  "operation_type": "duplicate",
  "created_at": "2022-09-30T18:13:53.140-03:00",
  "updated_at": "2022-09-30T18:13:53.175-03:00",\
  "template_data": {
    "total_value": "1000,00",
    "installments": "24",
    "bank_name": "Itau",
    ...
  },
  "batch": {
    "id": 3,
    "status": "signing",
    "number": "508",
    "quantity": 1,
    "quantity_approved": 1
  },
  "documents": [
    {
      "id": 23,
      "key": "fadef9ce-0f28-4792-bb3f-6d0bd5c6a055",
      "status": "created",
      "created_at": "2022-10-27T09:44:50.800-03:00",
      "updated_at": "2022-10-27T09:46:45.968-03:00",
      "file": null
    }
  ],
  "url": "https://app.securities.com.br/api/v1/assignments/1"
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
            "arrangement_id": 1,
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
  "arrangement_id": 1,
  "batch_id": 3,
  "number": "123456",
  "issue_date": "2022-09-30",
  "status": "pending",
  "full_amount": "100.0",
  "operation_type": "duplicate",
  "created_at": "2022-09-30T18:13:53.140-03:00",
  "updated_at": "2022-09-30T18:13:53.175-03:00",
  "batch": {
    "id": 3,
    "status": "signing",
    "number": "508",
    "quantity": 1,
    "quantity_approved": 0
  },
  "documents": [
    {}
  ],
  "url": "https://app.securities.com.br/api/v1/assignments/1"
}
```

Esse endpoint cria um termo de cessão

### HTTP Request

`POST https://app.securities.com.br/api/v1/assignments`

### Parâmetros da requisição

| Parâmetro      | Obrigatório | Tipo    | Descrição                                        |
|----------------| ----------- | ------- |--------------------------------------------------|
| arrangement_id | sim         | integer | ID do Arranjo da cessão                          |
| number         | sim         | string  | Número do termo de cessão                        |
| issue_date     | sim         | boolean | Data de emissão                                  |
| full_amount    | sim         | float   | Valor do termo (soma de todos os títulos)        |
| batch_id       | sim         | integer | ID do Lote de CCBs                               |

### Validações

O valor inserido em `full_amount` não é validado, ou seja, se inserir um valor diferente da soma dos valores dos títulos
poderá ter divergências. O motivo da não validação é porque o valor negociado pode ser menor que o valor da soma dos títulos,
sendo assim, não há com que comparar os valores inseridos, sendo esperado, em alguns casos, alguma divergência.
