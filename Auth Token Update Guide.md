n8n workflow : https://internalwf.zuper.co/workflow/UHoatWNUxJ0xu96J

Step 1: Generate Authentication Token for Internal Admin
- Hit the below api to generate the token. 
- Update email and password 
```
curl --location 'https://internaladminv2.zuperpro.com/api/account/login?region-code=apac-staging' \
--header 'User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:143.0) Gecko/20100101 Firefox/143.0' \
--header 'Accept: application/json, text/plain, */*' \
--header 'Accept-Language: en-US,en;q=0.5' \
--header 'Accept-Encoding: gzip, deflate, br, zstd' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer null' \
--header 'Origin: https://internaladmin.zuperpro.com' \
--header 'Sec-GPC: 1' \
--header 'Connection: keep-alive' \
--header 'Referer: https://internaladmin.zuperpro.com/' \
--header 'Sec-Fetch-Dest: empty' \
--header 'Sec-Fetch-Mode: cors' \
--header 'Sec-Fetch-Site: same-site' \
--header 'Priority: u=0' \
--header 'Pragma: no-cache' \
--header 'Cache-Control: no-cache' \
--data-raw '{
    "email": "<enter your email>",
    "password": "<internal admin login password>",
    "two_fa_secret_key": "<internal admin login key>",
    "expires_in": "7d"
}'
```
- from the response copy the "token"
- ![[Pasted image 20251023180808.png]]


Step 2: Update the token in n8n
- Go to Config node and replace the AUTH_TOKEN with the new token generated
- ![[Pasted image 20251023180938.png]]
- Save worflow