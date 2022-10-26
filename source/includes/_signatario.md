# Signatário

**TODO:** O signatário é utilizada para....

## Listar signatários

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/signers \
     -H "Authorization: Bearer $TOKEN"
```

```shell
curl -X GET https://app.securities.com.br/api/v1/documents/:document_id/signers \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "signers": [
    {
      "id": 1,
      "full_name": "John Carter",
      "has_documentation": false,
      "documentation": null,
      "email": "signer@example.com",
      "birthday": "1987-09-09",
      "phone_number": "(16) 98234-3045",
      "auth": "email",
      "communicate_by": "email",
      "key": "690e1c32-7edd-48e4-b083-a738f05b4d7e",
      "sign_as": "sign",
      "created_at": "2022-09-08T15:37:05.189-03:00",
      "updated_at": "2022-09-15T15:26:18.880-03:00"
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

Esse endpoint lista todos os signatários

### HTTP Request

Todos os signatários

`GET https://app.securities.com.br/api/v1/signers`

<br>Signatários por documento

`GET https://app.securities.com.br/api/v1/documents/:document_id/signers`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição |
| --------- | ------- | --------- |
| page      | integer | Paginação |

## Obter signatário

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/documents/:document_id/signers/:id \
     -H "Authorization: Bearer $TOKEN"
```

```shell
curl -X GET https://app.securities.com.br/api/v1/signers/:id \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "signer": {
    "id": 1,
    "full_name": "John Carter",
    "has_documentation": false,
    "documentation": null,
    "email": "signer@example.com",
    "birthday": "1987-09-09",
    "phone_number": "(16) 98234-3045",
    "auth": "email",
    "communicate_by": "email",
    "key": "690e1c32-7edd-48e4-b083-a738f05b4d7e",
    "sign_as": "sign",
    "created_at": "2022-09-08T15:37:05.189-03:00",
    "updated_at": "2022-09-15T15:26:18.880-03:00"
  }
}
```

Esse endpoint obtem todos os dados de um signatário

### HTTP Request

Obter signatário

`GET https://app.securities.com.br/api/v1/signers/:id`

<br>Obter signatário de um documento

`GET https://app.securities.com.br/api/v1/documents/:document_id/signers/:id`

## Criar signatário

> Request:

```shell
curl -X POST https://app.securities.com.br/api/v1/documents/:document_id/signers \
     -H "Authorization: Bearer $TOKEN" \
     -H "Content-Type: application/json" \
     -d '{
        "signer": {
          "email": "fulano@example.com",
          "auths": ["email"],
          "full_name": "Marcos Zumba",
          "has_documentation": true,
          "documentation": "123.321.123-40",
          "birthday": "1983-03-31",
          "phone_number": "11999999999",
          "sign_as": "sign",
          "communicate_by": "email"
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
  "signer": {
    "id": 4,
    "full_name": "Marcos Zumba",
    "has_documentation": true,
    "documentation": "123.321.123-40",
    "email": "fulano@example.com",
    "birthday": "1983-03-31",
    "phone_number": "11999999999",
    "auth": "email",
    "communicate_by": "email",
    "key": null,
    "sign_as": "sign",
    "created_at": "2022-09-16T18:41:00.079-03:00",
    "updated_at": "2022-09-16T18:41:00.079-03:00"
  }
}
```

Esse endpoint cria um signatário

### HTTP Request

Criar signatário avulso

`POST https://app.securities.com.br/api/v1/signers`

<br>Criar signatário vinculado a um documento

`POST https://app.securities.com.br/api/v1/documents/:document_id/signers`

### Parâmetros da requisição

| Parâmetro         | Obrigatório | Tipo    | Descrição                                                     |
| ----------------- | ----------- | ------- | ------------------------------------------------------------- |
| full_name         | sim         | string  | Nome completo                                                 |
| has_documentation | não         | boolean | Tem documentação, como CPF, CNPJ ou Passaporte. Padrão é TRUE |
| documentation     | condicional | string  | CPF, CNPJ ou Passaporte                                       |
| birthday          | condicional | string  | Data de nascimento                                            |
| email             | condicional | string  | E-mail                                                        |
| phone_number      | sim         | string  | Numero de telefone                                            |
| auth              | sim         | string  | Tipo de autenticação: "email"                                 |
| communicate_by    | sim         | string  | Por onde será notificado: "email"                             |
| sign_as           | sim         | string  | Assinar como: sign, party, witness, contractor, contractee... |
