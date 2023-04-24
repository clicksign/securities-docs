# CCB

CCB é a Cédula de crédito bancário: A Cédula de Crédito Bancário é título de crédito emitido por emissor-devedor em favor de instituição financeira, representando promessa de pagamento em dinheiro, decorrente de operação de crédito, de qualquer modalidade. Sobre a regulação da CCB, vide o art. 26 da Lei 10.931/2004.

Em outras palavras, a CCB é o que representará um crédito tomado e que foi assinado pelo tomador para que possa ser negociado como um título no mercado financeiro.

## Listar CCBs

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/securities \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "securities": [
    {
      "id": 2,
      "number": "123456",
      "issuer_full_name": "Hugo Fonseca",
      "issuer_document": "630.427.604-48",
      "installments": 1,
      "created_at": "2022-09-15T15:27:00.691-03:00",
      "updated_at": "2022-09-15T15:27:00.691-03:00",
      "url": "https://app.securities.com.br/api/v1/securities/2"
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

Esse endpoint lista todas as CCBs

### HTTP Request

`GET https://app.securities.com.br/api/v1/securities`

### Parâmetros de consulta

| Parâmetro | Tipo    | Descrição     |
| --------- | ------- | ------------- |
| number    | string  | Número da CCB |
| page      | integer | Paginação     |

## Obter CCB

> Request:

```shell
curl -X GET https://app.securities.com.br/api/v1/securities/:id \
     -H "Authorization: Bearer $TOKEN"
```

> Response:

```shell
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "security": {
    "id": 2,
    "number": "123456",
    "issuer_full_name": "Hugo Fonseca",
    "issuer_document": "630.427.604-48",
    "installments": 1,
    "signature_provider": "clicksign",
    "created_at": "2022-09-15T15:27:00.691-03:00",
    "updated_at": "2022-09-15T15:27:00.691-03:00",
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
    "url": "https://app.securities.com.br/api/v1/securities/2"
  }
}
```

Esse endpoint obtém todos os dados de uma CCB

### HTTP Request

`GET https://app.securities.com.br/api/v1/securities/:id`

## Criar CCB já assinada para Cessão

> Request:

```shell
curl -v POST https://app.securities.com.br/api/v1/securities \
     -H "Authorization: Bearer $TOKEN"
     -F "file=@file1.pdf"
     -F "signed=true"
     -F "signature_provider=govbr"
     -F "number=37891673"
     -F "installments=12"
     -F "issuer_full_name=Hugo Fonseca"
     -F "issuer_document=04218776143"
     -F "document_data={\"car\": \"Volkswagen\"}"

```

> Response:

```shell
HTTP/1.1 201 OK
Content-Type: application/json; charset=utf-8
```

```json
{
  "security": {
    "id": 2,
    "number": "123456",
    "issuer_full_name": "Hugo Fonseca",
    "issuer_document": "630.427.604-48",
    "installments": 1,
    "signature_provider": "clicksign",
    "created_at": "2022-09-15T15:27:00.691-03:00",
    "updated_at": "2022-09-15T15:27:00.691-03:00",
    "documents": [
      {
        "id": 23,
        "key": "fadef9ce-0f28-4792-bb3f-6d0bd5c6a055",
        "status": "validated",
        "created_at": "2022-10-27T09:44:50.800-03:00",
        "updated_at": "2022-10-27T09:46:45.968-03:00",
        "file": {
          "url": "https://example.com/path/to/document.pdf"
        }
      }
    ],
    "url": "https://app.securities.com.br/api/v1/securities/2"
  }
}
```

Endpoint que recebe títulos CCBs já assinados pelo tomador fora dos produtos Clicksign, mas que serão cedidos na Clicksign Securities.

<aside class="notice">
Este endpoint tem como funcionalidade a recepção de CCBs que serão endossadas e cedidas pela Clicksign Securities, porém, o seu registro não ocorreu nos produtos Clicksign, ou seja, receberemos aqui uma CCB (.pdf) previamente registrada e assinada por produtos terceiros.

Caso o objetivo seja de criar uma CCB, registrando-a na Clicksign Securities para então também ser cedida com nossos produtos, agora ou no momento oportuno de movimentação do estoque de títulos, consulte nossa API de Proposta (título antes de se tornar uma CCB assinada pelo tomador).
</aside>

### HTTP Request

`POST https://app.securities.com.br/api/v1/securities`

### Parâmetros

Essa requisição deve ser um `multipart/form-data` com os seguintes parâmetros:

| Parâmetro             | Tipo    | Descrição                                                                       |
| --------------------- | --------| ------------------------------------------------------------------------------- |
| file                  | File    | Upload do pdf que será anexado a CCB                                            |
| signed                | boolean | Boolean indicando se o pdf fornecido está assinado                              |
| signature_provider    | Enum    | String indicando qual assinador foi utilizado. Ver assinadores aceitos abaixo.  |
| number                | string  | Número da CCB                                                                   |
| issuer_full_name      | string  | Nome completo do emitente                                                       |
| issuer_document       | string  | Documento do emitente                                                           |
| installments          | integer | Número de parcelas                                                              |
| document_data         | string  | Serialização do json com os dados do documento para compor a CCB                |

### Assinadores suportados

Lista de assinadores suportados no momento:

| Parâmetro (utilizar na request) | Nome de exibição    |
| ------------------------------- | --------------------|
|d4sign | D4Sign |
|zapsign | ZapSign |
|docusign | Docusign |
|totvs | Assinatura eletrônica TOTVS |
|autentique | Autentique |
|assinebem | Assine Bem |
|contraktor | Contraktor |
|juridoc | Juridoc |
|santocontrato | Santo Contrato |
|certisign | Certisign |
|signnow | SignNow |
|adobesign | Adobe Sign |
|hellosign | Hello Sign |
|webdox | Webdox |
|sdocsafe | Sdoc Safe |
|accesscorp | Access Corp |
|ebox | eBox Digital |
|arquivar | Arquivar |
|unico | Unico |
|formalizar | Formalizar e-Signature |
|onedoc | 1Doc |
|bry | Bry |
|quicksoft | QuickSoft |
|fepweb | FepWeb |
|govbr | Gov.br |
|flexdoc | Flexdoc |
|brysigner | Bry Signer |
|besign | Besign |
|letssign | LetsSign |
|assertiva | Assertiva |
|optime | Optime |
|digicert | Digicert |
|qcertifica | Q Certifica |
|fast4sign | Fast4Sign |
