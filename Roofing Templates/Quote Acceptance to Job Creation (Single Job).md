

# Settings

## Field Options
- fieldType : 
	- described below
- value:
	- user selected value for a field
- required: true | false
	- used to validate missing required fields
- delimiter : 
	- used to combine the final output in case of dynamic fields

## Field Types

#### dynamic
- Any key from the source module can be used
- Allows chaining of keys using comma
	- "organization.organization_name, proposal_title"
- If multiple keys are chained, then user has the option to choose which delimiter should be used to combine the result
- deep object keys can be used by using '.'
	- eg: "organization.organization_name"

#### static
- Any hard coded text value can be used
	- eg: "any random text"

#### customField
- Any label of custom field from the source module can be used

## Variables Used

#### zwb_jj_job_category
- The job category name under which the new job should be created

#### zwb_qj_due_date_in_days
- the buffer days for the due date of job being created
	- eg: if the value is set as 10, then the due date of job will be set to --> current date + 10 days

#### ZUPER_API_KEY
- api key to be used for automation

#### ZUPER_API_REGION
- deployed region of the customer 

#### ZUPER_COMPANY_TIMEZONE
- timezone keyword for the company timezone


## User Customizable Fields  

- Job Category
	- required : true
- Job Due Date
	- required: true
- Job Title
	- required: true


# Failure Conditions

- Quote is Not in Approved Status
- Failed to find a match for Job Category using the settings user provided
- Missing required Field
- Invalid fieldType used


## Fields Copied From Quote:

- customer
- organization
- service address
- billing address
- line items


# Process

-  When quote is moved to APPROVED status, create a job based on the Settings chosen
	



