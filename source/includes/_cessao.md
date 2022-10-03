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
            "batch": {
              "quantity": 1,
              "securities": [
                {
                  "number": "123456"
                }
              ]
            }
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
full_amount              | não         | float    | Valor do termo (soma de todos os títulos). Padrão é ZERO
batch.quantity           | não         | integer  | Quantidade de títulos no lote. Padrão é ZERO
batch.securities.number  | não         | string   | Títulos que irão compor no lote

### Validações

O valor inserido em `full_amount` não é validado, ou seja, se inserir um valor diferente da soma dos valores dos títulos
poderá ter divergências. O motivo da não validação é porque o valor negociado pode ser menor que o valor da soma dos títulos,
sendo assim, não há com que comparar os valores inseridos, sendo esperado, em alguns casos, alguma divergência.

Se `batch.quantity` não for equivalente a quantidade total de títulos do lote, o processamento não será finalizado.

Em `batch.securities.number` será feito uma validação de unicidade do título. Num primeiro momento, será permitido inserir
um título usado em outro lote, o mesmo ficará com status `pending` e será adicionado a uma fila de validação de unicidade.
Após ser colocado na fila, o status será alterado para `checking`, após a validação, o status será alterado para `checked`
se for único ou para `failed` se estiver sendo usado em outro lote.

Sempre que um título for reprovado, com status `failed`, será gravado um log do motivo, e no final do todos os processamentos,
o operador do sistema terá acesso a um relatório de erros para saber os motivos e tomar as ações necessárias.
