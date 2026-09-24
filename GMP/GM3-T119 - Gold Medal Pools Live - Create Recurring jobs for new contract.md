
workflow: https://internalwf-ent.zuper.co/workflow/jsnHhSi7XA1NGuN6


## Triggers:
- contract status update
- contract update

## Constants:
- base url
- api key
- job category: Full Svc Maint Res [RM]
- customer category uid 

## Private App Changes 
- [x]  Property association is set as a mandatory check to create recurring jobs
- [ ] Used `recurring_rules?rule=$` endpoint to fetch recurring dates based on rule string instead of manually generating dates 
- [x] Added contract id to job title
- [x] Create customer in netsuite fix: customer name fix + customer category uid fix

## Edge Case
1. For Exit Condition #3 , we are using the first job returned from fetch jobs with contract filter. What if there are other jobs which are recurring jobs tagged to contract 
2. Dates are not formatted using moment
3. Recurrence dates are calculated manually instead of using API
4. Not fetching custom fields master 

## Exit Conditions
1. Inactivate Contract 
2. If there are already jobs created in contract AND trigger event is contract update AND contract end date is NOT updated  
3. If there are already jobs created in contract AND trigger event is contract update AND contract end date is NOT updated AND existing job is not a recurring job 
4. If contract status NOT CUSTOMER_APPROVED 
5. If Payment Information Verified custom field NOT "Yes"
6. If contract is expired

## Process
- wait node for contract update
- fetch contract
- exit if inactive contract
-  Exit If there are already jobs created in contract AND trigger event is contract update AND contract end date is NOT updated  
- Exit If there are already jobs created in contract AND trigger event is contract update AND contract end date is NOT updated AND existing job is not a recurring job 
- Fetch jobs for the contract (count 1) to check if there are jobs already created (NEED TO ADD ANOTHER FILTER TO CHECK RECURRING JOBS)
- If jobs found:
	- check exit conditions 4 to 6
	- If property associated to contract fetch it
	- Create recurring job payload:
		- if there is property associated to job and it has users assigned, they need to be assigned to job
		- Assets assigned to contract should be assigned to job
		- Push jobber number from contract ref_no to job custom field
		- Based on value of Contract custom field: Contract Type, determine the job category 
		- use recurrence start date = contract activation date OR contract start date. If start date less than today, set start date = today
		- use recurrence end date = contract end date
		- Fetch the recurrence rule info from contract custom fields 
			- Job Frequency
			- Job Weekday(s)
			- Job Day of Month
			- Job Interval
		- The recurrence dates should always be after today
	- Create recurring jobs
- Else :
	- If event is contract update and contract end date is updated:
		- check if recurring jobs already exists. If not exit flow
		- Update the recurring job series with updated data from contract
	- else:
		- exit flow