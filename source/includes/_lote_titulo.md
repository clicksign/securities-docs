# CCB em Lote

Endpoint utilizado para vincular a CCB a um Lote específico, permitindo futuras consultas de lastro da operação por completo, considerando seu ciclo de vida.

## Listar CCBs do lote

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
      "updated_at": "2022-10-06T16:46:40.889-03:00",
      "url": "https://app.securities.com.br/api/v1/batches/1/security_batches/1"
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

Esse endpoint lista todas as CCBs do lote

### HTTP Request

`GET https://app.securities.com.br/api/v1/batches/:batch_id/security_batches`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| page      | integer | Paginação |

## Obter uma CCB do lote

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

Esse endpoint obtem todos os dados de uma CCB de um lote

### HTTP Request

`GET https://app.securities.com.br/api/v1/batches/:batch_id/security_batches/:id`

## Adicionar CCB no lote

> Request:

```shell
curl -X POST https://app.securities.com.br/api/v1/batches/:batch_id/security_batches \
     -H "Authorization: Bearer $TOKEN" \
     -H "Content-Type: application/json" \
     -d '{
          "security_batch": {
            "security_data": {
              "number": "123456",
              "assignor_name": "Fulano",
              "cession_value": "2002.20",
              "number": "12346"
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

Esse endpoint adiciona uma CCB no lote

### HTTP Request

`POST https://app.securities.com.br/api/v1/batches/:batch_id/security_batches`

### Parâmetros da requisição

| Parâmetro     | Obrigatório | Tipo  | Descrição        |
|---------------| ----------- |-------|------------------|
| security_data | sim         | jsonb | metadados da CCB |

OBS: O parâmetro `security_data` deve conter o attributo `number` com o número da CCB.

### Validações

Não será permitido enviar uma CCB se não for criada uma cessão associada ao lote.

Enquanto `quantity` não for equivalente a quantidade total de CCBs do lote, o processamento não será finalizado,
o status iniciará em `pending`, irá para `checking` após adicionar o primeiro CCB no lote e, até que todas as
CCBs sejam enviadas, permanecerá nesse status.

Não será permitido enviar uma quantidade de CCBs maior que `quantity`.

Não será permitido enviar uma CCB que já esteja no lote.

<aside class="warning">
  <strong>Atenção</strong><br>
  Para obter o <code>security_id</code> será necessário <a href="#listar-ccbs">consultar pela CCB</a> no respectivo endpoint.
</aside>
