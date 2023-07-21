# Arranjo

Partes envolvidas no processo de compra e venda de uma operação financeira. São os stakeholders da operação de oferta e aceite de CCBs, que vão originar, enviar para assinatura do tomador e por fim, vender esses títulos aos fundos. Juntos, essas partes formam um arranjo que fazem negociações entre si e possuem contas de originação e destino dentro desse grupo.

## Listar Arranjos

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/arrangements \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "arrangements": [
    {
      "id": 120,
      "account_id": 7,
      "name": "Arranjo 1",
      "operation_type": "duplicate",
      "url": "https://app.securities.com.br/api/v1/arrangements/120"
    },
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

Esse endpoint lista todos os Arranjos nos quais a conta é cessionária

### HTTP Request

`GET https://app.securities.com.br/api/v1/arrangements`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| page      | integer | Paginação |

## Obter Arranjo

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/arrangements/:id \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "arrangement": {
    "id": 120,
    "account_id": 7,
    "name": "Arranjo 1",
    "operation_type": "duplicate",
    "signers": [
      {
        "id": 500,
        "full_name": "Bilck Endorser",
        "has_documentation": true,
        "documentation": "304.336.560-77",
        "email": "guilherme.bilck+endossante@clicksign.com",
        "birthday": "1981-08-17",
        "phone_number": "+5561999999999",
        "auth": "email",
        "communicate_by": "email",
        "key": "e19a0a2a-e245-45bc-a914-1c42c587cf45",
        "sign_as": "endorser",
        "selfie_enabled": false,
        "official_document_enabled": false,
        "liveness_enabled": false,
        "handwritten_enabled": false,
        "facial_biometrics_enabled": false,
        "created_at": "2023-03-08T15:05:45.342-03:00",
        "updated_at": "2023-03-08T15:05:45.499-03:00"
      }
    ]
  }
}
```

Esse endpoint obtém todos os dados de um Arranjo

### HTTP Request

`GET https://app.securities.com.br/api/v1/arrangements/:id`
