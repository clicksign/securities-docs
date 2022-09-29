# Arranjo

**TODO:** O Arranjo é utilizada para....

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
[
  {
    "id": 1,
    "account_id": 1,
    "member_id": 2,
    "member_type": "endorser"
  }
]
```

Esse endpoint lista todos os Arranjos

### HTTP Request

`GET https://app.securities.com.br/api/v1/arrangements`

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
  "id": 1,
  "account_id": 1,
  "member_id": 2,
  "member_type": "endorser",
  "signers": [
    {
      "id": 100,
      "account_id": 218,
      "document_type": "Proposal",
      "document_id": 99,
      "full_name": "Latia Pouros Roberts",
      "has_documentation": true,
      "documentation": "062.231.968-06",
      "email": "rufus@quitzon.co",
      "birthday": "1964-10-22",
      "phone_number": "(52) 91647-1229",
      "auth": "email",
      "communicate_by": "email",
      "created_at": "2022-09-29T14:18:21.007-03:00",
      "updated_at": "2022-09-29T14:18:21.007-03:00",
      "key": "9429903a-ba8d-4eca-be62-d5d034bd0f52",
      "sign_as": "sign",
      "link_key": "f122bf00-f6d8-4567-b305-d7163f4fda89",
      "batch_key": "3b751793-59b2-40a0-b421-758632ce28fe"
    },
    {
      "id": 101,
      "account_id": 220,
      "document_type": "Proposal",
      "document_id": 100,
      "full_name": "Pres. Edgar Nolan O'Reilly",
      "has_documentation": true,
      "documentation": "422.420.114-30",
      "email": "abdul@goodwin.name",
      "birthday": "1998-05-09",
      "phone_number": "(70) 95512-3125",
      "auth": "email",
      "communicate_by": "email",
      "created_at": "2022-09-29T14:18:21.014-03:00",
      "updated_at": "2022-09-29T14:18:21.014-03:00",
      "key": "89a2a6d1-86d2-4c0e-ad0c-9fffa31668d9",
      "sign_as": "sign",
      "link_key": "d4902434-9298-4aa0-8b63-4033272519f0",
      "batch_key": "43c64e4d-ac90-4698-a523-17f6225ae709"
    },
    {
      "id": 102,
      "account_id": 222,
      "document_type": "Proposal",
      "document_id": 101,
      "full_name": "Rep. Zachary Borer Feest",
      "has_documentation": true,
      "documentation": "559.451.638-72",
      "email": "fleta_bahringer@parisian.org",
      "birthday": "1976-12-06",
      "phone_number": "(48) 95809-7877",
      "auth": "email",
      "communicate_by": "email",
      "created_at": "2022-09-29T14:18:21.021-03:00",
      "updated_at": "2022-09-29T14:18:21.021-03:00",
      "key": "9c96c6aa-28fd-42d3-83b0-b20f46150c75",
      "sign_as": "sign",
      "link_key": "a0864d19-eac4-4172-91be-5f4a2fbeaa65",
      "batch_key": "51af2753-0a4e-4e05-8bd3-230cb94c41c6"
    }
  ]
}

```

Esse endpoint obtem todos os dados de um Arranjo

### HTTP Request

`GET https://app.securities.com.br/api/v1/arrangements/:id`
