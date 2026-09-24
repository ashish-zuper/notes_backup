
### SDK Commands

```
- initialize sdk client
- listen to app registered event
- create a button with title View Profitability
- get the button instance
- On button click : 
	- get job details and extract the response and get job_uid
	- create a configurable url
	- get auth_token, dc_api_url from localStorage
	- add job_uid, auth_token, dc_api_url as query params to the created url
	- open url in new tab
```

```
- set the base url to : https://staging.zuperpro.com/api/customer_portal/jobs?company_uid=d72d9c81-ce36-4c62-8242-e5a67cfef34f
```

```
- use functional programming to refactor code
```

```
- add comments and consoles for debugging
```

```
- create a high level summary of the feature implemented in index.js
```
### Generate POST SDK App

```
- create a nodejs script
- keep the base url, api key authentication as configurable
- take contents from index.js 
- then append it to the custom_code key in the body as described below
- use axios and the following api as reference

curl --location --request PUT 'https://stagingv2.zuperpro.com/api/misc/custom_code/ff041950-4c2a-4d4c-bb48-ef28ae0eb7fc' \
--header 'x-api-key: test' \
--header 'Content-Type: application/json' \
--data '{
        "custom_code":{
            "custom_code_uid": "ff041950-4c2a-4d4c-bb48-ef28ae0eb7fc",
            "custom_code_type": "JS",
            "is_v3":true,
            "custom_code": 
        }
    }'
```


