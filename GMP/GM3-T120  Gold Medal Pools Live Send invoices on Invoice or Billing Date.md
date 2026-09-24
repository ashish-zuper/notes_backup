WORKFLOW: https://internalwf-ent.zuper.co/workflow/S4gyfGOyEAC69Zki

## Triggers:
- contract new
- contract update

## Constants:
- base url
- api key

## Private App Changes 
- [ ] Not exiting for automation user
- [ ] Not executing for contract update  - not required

## Edge Case


## Exit Conditions
1. If triggered by automation user
2. If send_to_customer is false in invoice settings of contract

## Process
- Fetch contract
- Check exit conditions
- Update send_to_customer under invoice settings  as false and custom field: Send Invoices Automatically as Yes