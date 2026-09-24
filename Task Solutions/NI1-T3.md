## Proposed Solution

### Methods Needed
1.  Zuper Workflow
2. Automation

#### Zuper Workflow
- Trigger: Request Status Update
- Trigger Status: Approved
- Process:
	- Choose create Job ACTION with the following hardcoded values
		- Job Title: *Job From Request*
		- Job Category: Choose any Random Category (this will later be changed via automation)
		- Due Date: Choose 30 days form current date

#### Automation 
- Trigger: New Job
- Process:
	- Check if there is a request attached to job 
	- If no then no operation
	- Update the job data with the following mapping:
		- Job Title --> Request Title
		- Job Category --> Request Category
		- Job Description --> Request Description 
		- Job Attachments --> Request Attachments