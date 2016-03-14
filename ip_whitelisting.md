# IP Whitelisting


Some services may prevent unauthorized access to their servers. Only whitelisted IP addresses are allowed to connect. For instance, Booking.com is asking to enter source IPs.

Please use the following IP addresses for whitelisting:

| Name | Address |
| -- | -- |
| pilot.datatrans.biz (Test) | 193.16.220.3 |
| payment.datatrans.biz (Production) | 193.16.220.152 |
| payment.datatrans2.biz (Production Backup) | 91.223.186.4  |
| sftp.datatrans.biz (SFTP Production) | 193.16.220.16 |


Depending on how restrictive you want to setup the whitelist, you can also whitelist our full Class C networks. Especially sftp-proxy could switch to 91.223.186 subnet in case of a emergency. For a full Class C network whitelist, please use 193.16.220.0/24 and 91.223.186.0/24.




