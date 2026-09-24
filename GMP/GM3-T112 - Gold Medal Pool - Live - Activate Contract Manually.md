WORKFLOW: https://internalwf-ent.zuper.co/workflow/sjoKSQsHW8RitTrH

## Triggers:
- contract activate

## Constants:
- base url
- api key
- timezone
- recurring maintenance category uid

## Private App Changes 

- [x] Removed mandatory check of property for contract renewal  
## Edge Case


## Exit Conditions
- Triggered user = automation user

## Process
- Fetch contract
- Check if renewal required using contract end date and today
- If required renew contract 
- If not:
	- create recurring jobs
	- check service restart date custom field
	- if it is after today, then invoices should be generated
	- Create invoice:
		- generate invoice for each month from contract start - generate_invoice_days
		- add tax and discount from contract
