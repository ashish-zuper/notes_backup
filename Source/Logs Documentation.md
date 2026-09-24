### Statuses 
- INIT
- SUCCESS
- FAILED

### Log Types
- GET DATA
	- Job Category
	- Ticket
	- HS Pipeline
	- HS Company
	- HS Contact
	- HS Site
```javascript
    createLog(
      logger,
      PAGE,
      FUNCTION_NAME,
      "GET DATA - SUCCESS - Job category",
      `Ticket ID: ${HUBSPOT_TICKET_ID}. Execution ID: ${PAYLOAD?.app_configs?.execution_id}`
    );
```


- FIND DATA
	- Job
	- Organization

```javascript
    createLog(
      logger,
      PAGE,
      FUNCTION_NAME,
      "FIND DATA - INIT - Job",
      `Ticket ID: ${HUBSPOT_TICKET_ID}. Execution ID: ${PAYLOAD?.app_configs?.execution_id}`
    );
```

- ABORTING PROCESS
	- Associations Not Found
	- Mandatory Associations Missing
	- Failed to Fetch Site
	- Either Company or Contact is Mandatory
	- Failed to Create Property
	- Property Not Found
```javascript
    createLog(
      logger,
      PAGE,
      FUNCTION_NAME,
      "ABORTING PROCESS - Associations Not Found",
      `Ticket ID: ${HUBSPOT_TICKET_ID}. Execution ID: ${PAYLOAD?.app_configs?.execution_id}`
    );
```

- MESSAGE
	- Init Create Organization Payload
	- Organization Payload Created - HS Company: ${hubspotCompanyId}
	- Organization Already Exists - Organization UID: ${}
	- Init Create Customer Payload - HS Contact: ${hubspotContactId}
	- Customer Payload Created - HS Contact: ${hubspotContactId}
	- Init Generate Job Custom Fields
	- Job Custom Fields Generated
	- Validating Job Not Created
```javascript
    createLog(
      logger,
      PAGE,
      FUNCTION_NAME,
      `MESSAGE - Init Create Organization Payload`,
      `Ticket ID: ${HUBSPOT_TICKET_ID}. Execution ID: ${PAYLOAD?.app_configs?.execution_id}`
    );
```

- CREATE DATA
	- SUCCESS - Organization - Organization UID: ${organizationUid}
	- INIT - Customer - HS Contact: ${hubspotContactId}
```javascript
    createLog(
      logger,
      PAGE,
      FUNCTION_NAME,
      `CREATE DATA - INIT - Organization`,
      `Ticket ID: ${HUBSPOT_TICKET_ID}. Execution ID: ${PAYLOAD?.app_configs?.execution_id}`
    );
```

- UPDATE DATA
	- Job
	- Ticket