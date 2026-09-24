
- Affected Event: All events (specifically noted in orphaned child job )
	- ![[Pasted image 20240801113824.png]]
	- Special characters are being added to address field in hubspot 
	- The value is added in Hubspot Contact property: county  (internal value)
	- Corresponding property in zuper: job address
	- The characters are not recognised as string by mysql parser and hence insert to db is failing
	- Due to no record in db, any further events are not being processed for the job
	- Sample Job : https://web.zuperpro.com/jobs/255b6c8c-fba8-463d-8f4e-224492825710/details
	- Ticket: https://app.hubspot.com/contacts/4023574/record/0-5/3041184113
