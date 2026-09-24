
### Get Properties API
```
curl --location 'https://staging.zuperpro.com/api/v2/customer_portal/property?page=1&count=10&filter.keyword=4' \
--header 'Authorization: Bearer <auth token>'
```

- Will only list properties linked to customer
- Not possible to view/list properties created for other customers

### Create Request API
```
curl --location 'https://staging.zuperpro.com/api/v2/customer_portal/request' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <auth token>' \
--data '{
    "request": {
        "request_title": "Validation Req 2",
        "request_description": "<p>Lorem ipsum dolor sit amet consectetur adipiscing elit, fermentum pellentesque dis risus augue nostra ornare ullamcorper</p>",
        "property_uid": "3f0324d0-5550-11ef-ab54-cfec33db84f6",
        "attachments": [],
        "service_address": {
            "city": "Chennai ",
            "state": "Tamil Nadu ",
            "geo_cordinates": [
                12.9729347,
                80.2512452
            ],
            "landmark": "",
            "street": "Zupersoft Solutions Private Limited, Rajiv Gandhi Salai, Elango Nagar, OMR",
            "country": "India",
            "zip_code": "600041"
        },
        "billing_address": {
            "city": "Chennai ",
            "state": "Tamil Nadu ",
            "geo_cordinates": [
                12.9729347,
                80.2512452
            ],
            "landmark": "",
            "street": "Zupersoft Solutions Private Limited, Rajiv Gandhi Salai, Elango Nagar, OMR",
            "country": "India",
            "zip_code": "600041"
        },
        "custom_fields": [],
        "request_preferred_date1": null,
        "request_preferred_date2": null
    }
}'
```

- Not possible to create request for properties which are not linked to customer
- ![[Pasted image 20240808184341.png]]


### Alternatives Tried
1. Tried to use admin auth token from zuper app instead of customer portal token
	- Status: Failed
	- Error: Invalid token
2. Create job directly instead of a request 
	- Status: Failed
	- Error: Customer Portal does not have api to create jobs


### Feasible Alternatives
- Build a customized customer portal and use Zuper API instead of Zuper Customer portal API for listing all properties and creating requests/jobs