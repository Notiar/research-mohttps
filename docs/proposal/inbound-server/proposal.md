# MoHTTPS Inbound Server Proposal

## Introduction

Inbound server is a server that receives emails from the internet and stores them in a database (to be read by client later).

## Endpoints

### POST /mohttpsapi/inbound/mail

Receives an email, does all integrity and security checks and stores it in a database.

#### Request details

- Authentication: `None`
- Method: `POST`
- Path: `/mohttpsapi/inbound/mail`
- Request body: [mail message](../mail-message.md)
- Request headers: `None`

#### Response details

- Status code: `200`
- Response body: `None`
- Response headers: `None`

#### Error responses

See [errors](../errors.md).

- Status code: `400`
- Valid codes:
  - `INVALID_MESSAGE` - Message is invalid
  - `MESSAGE_ALREADY_EXISTS` - Message already exists
  - `INTERNAL_ERROR` - Internal error
  - `SECURITY_ERROR` - Security error
- Response body: [error](../errors.md)

#### Inner workings

1. Message validation (see [mail message](../mail-message.md))
2. Message sender integrity checks (see [sender integrity](../security/sender-integrity.md))
3. Message storage
