# DNS records

| Record type | Record name                 | Value                                    | Description                                                                                                                                       |
| ----------- | --------------------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| TXT         | mohttps.<priority>.<domain> | ip or domain name of the inbound server  | Points to the IP address of the mail server with specified priority (lower number is higher priority).                                            |
| TXT         | mohttps.ps.<domain>         | ips or domain names of permitted senders | Comma separated list of IPs or domain names of permitted senders. Will run [sender integrity](./security/sender-integrity.md) checks agains them. |
