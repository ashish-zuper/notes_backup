### Step 1 - n8n
- Turn n8n Inactive
- n8n: https://internalwf-v3.zuper.co/workflow/iI7cl6mBKsH2Zy2Z

### Step 2 - Purge Queue
- Go to rabbitmq dashboard
- Click on awrs_netsuite under Tab: Queues and Streams 
- ![[Pasted image 20241220180146.png]]
- In the opened menu scroll to the down and click on Purge Messages
![[Pasted image 20241220180314.png]]

### Step 3 - Enable n8n
-  Turn n8n Active
- n8n: https://internalwf-v3.zuper.co/workflow/iI7cl6mBKsH2Zy2Z


### Step 4 - Run Scripts
- The following actions must be done in order
- node js has to be installed in the system to proceed
1. Open terminal in the folder where scripts are located
2. Run command : `npm i`
3. Run script 1
	1. Check if a file called executions.json exists in the directory
	2. If yes delete that file
	3. Run the script :  `node .\getExecutions.js`
	4. The following message will be shown once done
	5. ![[Pasted image 20241220180635.png]]
	6. A new file called executions.json will be created in the same directory
	7. Make sure this file is created successfully before going to next step
4. Run script 2
	1. If file errors.json exists, delete it
	2. Run the script :  `node .\triggern8n.js`
	3. Wait till you get the message All payloads have been sent
	4. ![[Pasted image 20241220181133.png]]
5. Check if errors.json is created
	1. If this file exists, these many executions failed and will have to be retired
6. Run script 3
	1. Run the script: `node .\failExecutions.js`
	2. This will mark all the executions as FAILED in db
	3. ![[Pasted image 20241220181441.png]]
