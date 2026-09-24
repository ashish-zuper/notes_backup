
## Script 1 : De-duplicate customer

1. Maintain an array of duplicate customer uids for lookup
2. Loop through each customer 
3. check if customer exists in the duplicate array already.
4. if yes skip customer and proceed to next customer
5. else :
6. do a filter to check if customer has  duplicates -- Apply customer duplicate logic
7. if not found, proceed to next customer
8. if duplicates found :
9. fetch associated jobs  and assets
10. fetch jobs associated to assets
11. validate if asset jobs and customer jobs match. if not flag for manual review
12. loop through duplicate customer and fetch associated jobs and assets
13. apply logic to find the latest instance of the customer 
14. update the duplicate assets and jobs to have the latest customer instance
15. create a report of all the customers flagged for merge
16. merge the duplicate customers to the latest instance 

## Script 2: De-duplicate Assets

1. Maintain an array for duplicate asset uids for lookup
2. Loop through each asset
3. check if exists in the duplicate array already
4. if yes skip asset and proceed to next 
5. check if a duplicate asset exists using filter
6. if not found proceed to next asset
7. if duplicate found:
8. fetch associated jobs
9. apply logic to find original asset
10. update jobs asset
11. create a report of all assets to be deleted
12. delete duplicate assets

## Script 3: Jobs without assets

1. Loop through each job
2. check if job does not have asset
3. check if asset serial available in cf
4. if not flag for manual review
5. check if asset exists using serial number 
6. if not found flag it
7. if found, associate to job

## Logic to Find Duplicate Customer
NOTE: Abo number can either be in last name field or in custom filed ABO Number 
1. Do keyword  search using abo number 
2. Do email filter + keyword search of first name + last name. then check if either abo number = same or abo number missing 
3. if either of above queries returned more than 1 result, consider them as duplicates
4. once duplicates array is formed, do another validation to check if 
5. Take the record with the latest updated_at value as the master and merge other customers 

## Logic to find duplicate asset
- Do keyword search using asset serial number
- if multiple records exist for same serial number, consider as duplicate 


## Reports to be created for Manual Review  (do this before running scripts)
1. Jobs where customer associated to job NOT EQUAL to the customer associated to asset in the job
2. Jobs where customer is missing
3. Jobs where asset info is missing (asset not linked to job and there is no Product Serial No in custom field )
4. Assets with same serial number and different customers


## Reports to be generated before running deletion/update scripts 
1. Duplicate Assets flagged for deletion 
2. Duplicate Customers flagged for merge 
3. Jobs where info will be updated

