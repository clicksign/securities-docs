# Duplicatas em Lote

Endpoints utilizados para vincular Duplicatas a um Lote específico, permitindo futuras consultas de lastro da operação por completo, considerando seu ciclo de vida.

## Listar Duplicatas do lote

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/batches/:batch_id/duplicates/security_batches \
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
      "url": "https://app.securities.com.br/api/v1/batches/1/duplicates/security_batches/1"
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

Esse endpoint lista todas as Duplicatas do lote

### HTTP Request

`GET https://app.securities.com.br/api/v1/batches/:batch_id/duplicates/security_batches`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| page      | integer | Paginação |

## Obter uma Duplicata do lote

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/batches/:batch_id/duplicates/security_batches/:id \
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

Esse endpoint obtém todos os dados de uma Duplicata de um lote

### HTTP Request

`GET https://app.securities.com.br/api/v1/batches/:batch_id/duplicates/security_batches/:id`

## Adicionar Duplicata no lote

> Request:

```shell
curl -X POST https://app.securities.com.br/api/v1/batches/:batch_id/duplicates/security_batches \
     -H "Authorization: Bearer $TOKEN" \
     -H "Content-Type: application/json" \
     -d '{
          "security_batch": {
            "security_data": {
              "number": "123456",
              "issuer_full_name": "Fulano",
              "issuer_document": "54194131000186",
              "total_value": 12554.42,
              "invoice": "551000125"
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

Esse endpoint adiciona uma Duplicata no lote

### HTTP Request

`POST https://app.securities.com.br/api/v1/batches/:batch_id/duplicates/security_batches`

### Parâmetros da requisição

| Parâmetro     | Obrigatório | Tipo  | Descrição              |
|---------------| ----------- |-------|------------------------|
| security_data | sim         | jsonb | metadados da Duplicata |

<aside class="warning">
  <strong>Atenção</strong><br>
  O parâmetro <code>security_data</code> deve conter os atributos <code>number</code>, <code>issuer_full_name</code>, <code>issuer_document</code>, <code>total_value</code> e <code>invoice</code> que são obrigatórios para o documento da Duplicata.
</aside>

### Validações

Não será permitido enviar uma Duplicata se não for criada uma cessão associada ao lote.

Enquanto `quantity` não for equivalente a quantidade total de Duplicatas do lote, o processamento não será finalizado,
o status iniciará em `pending`, irá para `checking` após adicionar a primeira Duplicata no lote e, até que todas as
Duplicatas sejam enviadas, permanecerá nesse status.

Não será permitido enviar uma quantidade de Duplicatas maior que `quantity`.

Não será permitido enviar uma Duplicata que já esteja no lote.

<aside class="warning">
  <strong>Atenção</strong><br>
  Diferentemente do lote de CCBs, as Duplicatas são geradas após a adição no lote, utilizando o modelo indicado no arranjo.
</aside>
