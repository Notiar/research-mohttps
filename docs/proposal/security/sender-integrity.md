# Sender integrity

To prevent sender spoofing, MoHTTPS uses sender integrity checks.

## How it works

1. Inbound server A receives a message (POST /mohttpsapi/inbound/mail)
2. Inbound server A processes the message (see [mail message](../mail-message.md))
3. Inbound server A retrieves the sender's email address from the message - for example `joe@server-b.example`
4. Inbound server A fetches DNS TXT mohttps.ps record for server B - in this case `mohttps.ps.server-b.example`
5. Inbound server A checks if the sender's email domain is included in the DNS TXT mohttps.ps record (for example `anything.example,server-b.example` will pass for `joe@server-b.example`)
6. In the case of failure, the message is rejected with `SECURITY_ERROR` error code
7. Inbound server A retrieves messageId and signature from the message and calculates checksum (see [mail message](../mail-message.md#signature), [checksum](../mail-message.md#checksum))
8. Inbound server A fetches DNS TXT mohttps.&lt;priority&gt; records for server B - in this case `mohttps.10.server-b.example`
9. Inbound server A calls POST /mohttpsapi/inbound/:messageId/integrity API endpoint on server B (retrieved from DNS TXT records -- this is critical for security) with the messageId, signature and checksum
10. Depending on the response, the message is either accepted or rejected with `SECURITY_ERROR` error code

## Outcomes

This check guarantees that:

- The sender server is authorized to send emails as this domain
- The sender server knows about the message (no one spoofed the sender)
- The message has not been tampered with
