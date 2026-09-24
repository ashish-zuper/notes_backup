- Can we bring dropdown button to bulk action 
	-  `Not Required`
- API to fetch all jobs in job listing page similar to .get("job")
	- `Not Required`
- Listen to modal events/set values in new pages (for eg. Open Products modal, set products filters )
	- `workaround using price list
- Ability to preview/render images in modals
	- `done
- Need to listen to associations in new pages
	- `done
- Need getter for new pages for form fields
	- `future sdk release

## Amway
- Cannot do :
	- [task url](https://projects.zoho.com/portal/zuperinc?canAddOACHeader=true&frameorigin=https://one.zoho.com#taskdetail/1832517000008685726/1832517000008676220/1832517000008880191) 
		- `workaround: implement using pricelist feature`
		- Cannot listen to update event of product description
		- cannot rename description
		- cannot make description a dropdown
		- cannot update the opened product data
	- [task url](https://projects.zoho.com/portal/zuperinc?canAddOACHeader=true&frameorigin=https://one.zoho.com#taskdetail/1832517000008685726/1832517000008676220/1832517000008880163)
		- `workaround: run a cron to sync qty and price from hybris + button for manual sync`
		- `action item: add additional variables support for setter and event lister for add products modal` 
		- Cannot listen to select product modal open
		- Cannot close the select product modal via sdk
## AWRS
- [task url](https://projects.zoho.com/portal/zuperinc?canAddOACHeader=true&frameorigin=https://one.zoho.com#taskdetail/1832517000004527161/1832517000008779348/1832517000009005652)
	- `done`
	- cannot show images in modal
	- cannot show table data (for parts and service)

## Gold Medal Pools
- [task url](https://projects.zoho.com/portal/zuperinc#taskdetail/1832517000006492159/1832517000008664613/1832517000009217662)
	- `workaround: remove deactivate contract permission in custom role`
	- Not able to do DOM manipulation to hide native buttons

## E & S Solutions
- Assisted scheduling in job details page
	- defer to product team
	- `future sdk release: use iframe modal to view filter`


## Action Items
1. Getter for new/edit page fields 
2. Additional variable support for new/edit page setter and event listeners:
	1. the variable which saves the products list in the add product modal
	2. the variables for the filters in the add product modal (location, category)
3. Communication between iframe to sdk *(no task dependency as of now) 

