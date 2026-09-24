	- [ ] Run the locale script in all regions
	- [x] staging
	- [ ] prod
- [x] recommend search -> complete word search, for best match if nothing can we get to other options?
- [ ] inspect order creation uom change
- [x] populate vendor cost in proposal template api, product group api  API-4395
- [ ] pre save hook to update is_supplier_integrated_product **hold**
- [x] API-3658
	- [x] fix the vendor_sku: it should be = variantCode
	- [x] is_supplier_imported_product boolean should be updated to true after import of each product
	- [x] upsert the imported supplier info into associated_supplier_provider array after import complete
	- [x] linked_catalog_uids should be updated with the catalog uid after import
	- [x] analyze what happens when: supplier product only has single variant and the variant is N/A
- [ ] API-4308
	- [ ] Until fulfilled status , we should allow to edit the PO status
	- [ ] Purchase cost is changing based on the base price and should be verified -> after marking as submitted
	- [x] supplier order id column need to be added in the listing
- [ ] API-4312
	- [ ] Notify PO creator when status is '_Delivered_'
	- [ ] PO status such as Invoiced must be updated along with invoice attachment
	- [ ] All other reverse status/updates from SRS must happen on Zuper PO
	- [ ] Mark as invoiced must be relaxed from both back and frontend
		- [ ] Allow PO edit in ALL status until Fulfilled
- [x] first fetch the active branch api to get the products.  then only import using the active branch variant uom. use same uom for all variants 
- [ ] show error message if the product is not available for the current preferred branch
- [ ] check if we are showing the active branch products of preffered branch



- [x] the catalog should not be created if:
	- during the srs price api if in the api response the message shows: Item not Found. This item does not exist in the SRS Catalog.
	- skip catalog creation for that branch for that product uom combo if the price api responds with the metioned message. sharing the price api response below

PO
- [ ] check price update
- [ ] check if total price updated properly
- [ ] remove user from the po srs activities 
- [ ] normalize all po activities to have supplier type
- [ ] during po creation for pricing, if we get item not found then should we throw error
- [ ] in the custom line item view we need an api which will fetch the branch products instead of catalog products 
- [ ] create an indicator after send to vendor to block further retry
- [ ] attach the the invoice pdf to invoice status metadata



Edit PO 
- to Draft
	- restrict after Send to Vendor

Line Item Update
- 

Cancelled Status
- restrict after sent to vendor for integrated vendor

Delete PO, Rollup Po
- restrict after sent to vendor for integrated vendor


Removed statuses:
- Delivered

Should not send public url if integrated vendor 