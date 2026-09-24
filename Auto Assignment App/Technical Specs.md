
# Categories

### 1. Availability and Scheduling

- Availability
- Workhours
- Comp off
- Time to commute (reach and return)
- Scheduled time

### 2. Location and Proximity

- Closest person nearby that location
- Proximity of job location
- Service territory
	- Zip code
	- Geo coordinates
	- Geo fencing
- Provision to choose Address field
	- Service Address or Billing Address

### 3. User and Role Information

- Default User
	- Single User
	- Multiple Users with assignment priority
- User who created the job
- Default Team

### 4. Skills and Qualifications

- Skills
- Category/Job Category

### 5. Custom Field Based

- User Custom Field
- Asset Custom Field



# Configurations

### 1.  Availability and Scheduling
- Consider Workhours
	- Assigns to the FE with the lowest hours in the week
	- Field Type : dropdown
	- Option: Yes, No
- Consider Comp off
	- Do not assign to FE if on leave
	- NOTE: Need to validate if assisted scheduling api does this by default
	- Field Type : dropdown
	- Option: Yes, No
- Enable Reschedule
	- Reschedule the job based on FE available slot
	- Field Type : dropdown
	- Option: Yes, No
- Multi - day jobs
	-  Needs Discussion as Assisted Scheduling API will not be able to handle this

### 2. Location and Proximity
- Choose Service Territory Type
	- Field Type: dropdown
	- Options:
		- Zip code
		- Geo coordinates
		- Geo fencing
		- Both Zip code and geo fencing (in this case we will need to send 2 apis)
- Which address to consider
	- Dependent Field (Choose Service Territory Type)
	- Field Type: dropdown
	- Options: Service Address or Billing Address
- Proximity Settings
	- Assign to nearest user from job
		- Field Type : dropdown
		- Option: Yes, No
	- How to get User Location
		-  Dependent Field (Assign to nearest user from job)
		-  Field Type : dropdown
		- Option: From previous job or User custom field
	- User Custom Field Name
		- Dependent Field (How to get User Location)
		- Field type: text

### 3. User Role Information
- Assign to Default User
	- Field Type: Multi select field
	- User priority will be based on selected order
- Assign to Default Team
	- Field Type: Multi select field
- Assign to created user
	- Field Type: text
	- This should be considered to be done via workflow 

### 4. Skills and Qualifications
- Should consider skills?
	-  Field Type : dropdown
	- Option: Yes, No
- Skill filter type
	- Dependent field (Should consider skills? )
	- Field Type: dropdown
	- Options: All Chosen Skills OR Any of the Chosen Skills
- Should consider skill percentage
	-  Field Type : dropdown
	- Option: Yes, No
- Skill percentage threshold 
	- Field type: text input
- Should consider skill expiry
	-  Field Type : dropdown
	- Option: Yes, No

### 5. Custom Field Settings
- Should Assign based on custom field?
	-  Field Type : dropdown
	- Option: Yes, No
- Select Module
	- Dependent Field (Should Assign based on custom field?)
	- Field Type: dropdown
	- Asset
	- Property
	- Org
	- Customer
	- User
- Custom Field Label:
	- Field Type: Text
	-  Dependent Field (Select Module)
- Custom Field Type:
	-  Dependent Field (Select Module)
	- Field Type: dropdown
	- Options
		- User Name (assign from module linked to job)
		- External ID 
- External ID Custom Field in Job
	- Dependent Field (Custom Field Type = External ID)
	- Field Type: Text

### 6. Additional Settings
- Select Module
	- Field Type: dropdown
- Select Field Type:
	- Field Type: dropdown
	- Custom/default
- Select Field Label
	- Field Type: Text
- Select Field Data Type
	- Field Type: dropdown
	- Number
	- Text
	- Date
- Select Condition
	- Field Type: dropdown
	- Equal to 
	- Less than
	- Greater than
	- less than or equal to
	- greater than or equal to
- Select Comparison field type from Job
	- Field Type: dropdown
	- Default/custom
- Comparison Field Label
	- Field Type: Text
- NOTE: Using this setting we can setup additional conditions like Visa Expiration Custom Field(VEGA)
	