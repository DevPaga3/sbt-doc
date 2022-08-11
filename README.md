
# Paga3 API

API de integração na camada de middleware da Plataforma da Paga3


#### integração TelcoSMS
```http
  POST /api/v1/telcosms-sender
```
| Parâmetro   | Tipo       | Descrição                           |
| :---------- | :--------- | :---------------------------------- |
| `api_key_app` | `string` | **Obrigatório**. A chave da sua API |
| `cell_phone` | [`string`] | **Obrigatório**. Um array de string |
| `message_body` | `string` | **Obrigatório**. Corpo da mensagem |

#### Retorna a quantidade de mensages enviadas.
```javascript
{
  api_key_app:  'ttsttw66wyhwhghwsjjJAHy2',
  cell_phone:   '923000999' or ['923000999', '913098098'],
  message_body: 'Saudações, Seja benvindo à Paga3'
}
```

#### integração Wesender
```http
  POST /api/v1/wesender-sender
```
| Parâmetro   | Tipo       | Descrição                                   |
| :---------- | :--------- | :------------------------------------------ |
| `ApiKey` | `string` | **Obrigatório**. A chave da sua API |
| `Destino` | [`string`] | **Obrigatório**. Um array de string |
| `Mensagem` | `string` | **Obrigatório**. Corpo da mensagem |
| `CEspeciais` | `boolean` | Identificação da existencia de caracter especiais |

#### Retorna a quantidade de mensages enviadas.
```javascript
{
  ApiKey:       'ttsttw66wyhwhghwsjjJAHy2',
  Destino:      '923000999' or ['923000999', '913098098'],
  Mensagem:     'Saudações, Seja benvindo à Paga3',
  CEspeciais:   true //Por default o valor é false
}
```

#### integração MINJ - NIF
```http
  GET /api/v1/minj-nif
```

| Parâmetro   | Tipo       | Descrição                                   |
| :---------- | :--------- | :------------------------------------------ |
| `token_paga3` | `string` | **Obrigatório**. A chave da sua API |
| `nif` | `string` | **Obrigatório**. Número de Identificação a buscar |

#### Retorna o número de Identificação inserido no body, se existir.
```javascript
{
  token_paga3:  'ttsttw66wyhwhghwsjjJAHy2',
  nif:   '09585LA0039399303',
}
```

#### integração AWS-SSE, SENDGRID
A integração de notificações por email é distribuído por dois serviços que trabalham em segundo plano, onde na camada de micro-serviços da aplicação Paga3 têm a mesma configuração para os dois serviços.

```http
  GET /api/v1/mailer-sender
```
| Parâmetro   | Tipo       | Descrição                                   |
| :---------- | :--------- | :------------------------------------------ |
| `token_api` | `string` | **Obrigatório**. A chave da sua API |
| `from` | `string` | **Obrigatório**. Remetente |
| `to` | `string` | **Obrigatório**. Destinatário |
| `subject` | `string` | **Obrigatório**. Assunto do Email |
| `content` | `string` | **Obrigatório**. Corpo do e-mail a ser enviado |

#### É enviado os paramentros na camada de middleware, e ela é responsável em definir qual dos serviços vai enviar o e-mail, por ordem de chegada, disponibilidade.
```javascript
{
  token_api:  'ttsttw66wyhwhghwsjjJAHy2',
  from:       'suporte@paga3.com',
  to:         'teste@gmail.com',
  subject:    'Notificação de pagamento da ultima prestação',
  content:    'Caro cliente Paga3,por meio desta informamos que...'
}
```
