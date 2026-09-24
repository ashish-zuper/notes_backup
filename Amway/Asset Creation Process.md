
## Asset Creation Process


## Credentials 

- BASE URL: https://amway-indonesia.zuperpro.com/dashboard
- company login name: amway-indonesia
- email: onboarding@zuper.co
- Password: 123456789

## Asset Creation

1. Search the product using product sku (column D)
2. Product category = asset category  (category_name will be same using that find from asset category master)
3. fetch asset info from gwms using the product serial number (column E)
```curl
curl 'https://apps.zuperpro.com/app/amway_indonesia/run?company_id=515&serial_number=<asset_serial_number>&type=SEARCH_GWMS_ASSET' -H 'Accept: application/json, text/plain, */*' -H 'Accept-Language: en-US,en;q=0.5' -H 'Accept-Encoding: gzip, deflate, br, zstd' -H 'Authorization: Bearer <token>' 
```
1. Payload to create asset 
``` javascript
const asset = this.gwmsassetresponse;

assetName = asset["BaseName"];

assetCode = asset["BaseSku"];

assetSerialNo = asset["SerialNumber"];

purchaseDate = asset["RegistrationDate"] ? this.datePipe.transform(asset["RegistrationDate"],"yyyy-MM-dd HH:mm:ss"): "";

warrantyExpiry = asset["WarrantyEnd"] ? his.datePipe.transform(asset["WarrantyEnd"], "yyyy-MM-dd HH:mm:ss")
: "";

placedInService = asset["WarrantyStart"]
? this.datePipe.transform(asset["WarrantyStart"],"yyyy-MM-dd HH:mm:ss")
: "";

orderingABO = asset["OrderingAboNumber"];

orderNumber = asset["OrderNumber"];

warrantyType = asset["WarrantyType"];

migrationStatus = "";

countryCode = asset["CountryCode"];

componentRemark = asset["ComponentRemark"]; //need to validate if this is returned in api

dateOfSale = this.datePipe.transform(asset["DateOfSale"], "yyyy-MM-dd"); //need to validate if this is returned in api

name = asset["Name"]; //need to validate if this is returned in api


mobile = asset["Mobile"]; //need to validate if this is returned in api


registrationDate = this.datePipe.transform(
asset["RegistrationDate"],"yyyy-MM-dd"); //need to validate if this is returned in api


email = asset["Email"]; //need to validate if this is returned in api


registrationDeadline = this.datePipe.transform(
asset["RegistrationDeadline"],
"yyyy-MM-dd"
); //need to validate if this is returned in api

```


```javascript
let assetCreationPayload = {

asset: {

asset_code: assetCode,

asset_name: assetName,

asset_quantity: 1,

asset_inspection_form: null,

...(assetSerialNo && { asset_serial_number: assetSerialNo }),

asset_location: {},

useful_life: {

type: "YEARS",

},

customer: <get customer from job>,

purchase_price: 1,

asset_category: <find asset category using product category>,

...(productuid && { asset_product: productuid }),

asset_parts: [],

...(purchaseDate && { purchase_date: purchaseDate }),

...(warrantyExpiry && { warranty_expiry_date: warrantyExpiry }),

...(placedInService && { placed_in_service: placedInService }),

custom_fields: [

{

label: "Ordering ABO Number",

value: orderingABO,

type: "SINGLE_LINE",

hide_to_fe: false,

read_only: false,

hide_field: false,

},

{

label: "Order Number",

value: orderNumber,

type: "SINGLE_LINE",

hide_to_fe: false,

read_only: false,

hide_field: false,

},

{

label: "Warranty Type",

value: warrantyType, // find this based on warranty start and end values

type: "SINGLE_LINE",

hide_to_fe: false,

read_only: false,

hide_field: false,

},

{

label: "Asset Migration Status",

value: migrationStatus,

type: "SINGLE_LINE",

hide_to_fe: false,

read_only: false,

hide_field: false,

},

{

label: "Country Code",

value: countryCode, 

type: "SINGLE_LINE",

hide_to_fe: false,

read_only: false,

hide_field: false,

},

  

{

label: "Component Remark",

value: componentRemark,

type: "SINGLE_LINE",

group_uid: environment.asset.customFieldsGroups.GWMSInfo.uid,

group_name: environment.asset.customFieldsGroups.GWMSInfo.name,

hide_to_fe: false,

read_only: false,

hide_field: false,

},

{

label: "Name",

value: name,

type: "SINGLE_LINE",

group_uid: environment.asset.customFieldsGroups.GWMSInfo.uid,

group_name: environment.asset.customFieldsGroups.GWMSInfo.name,

hide_to_fe: false,

read_only: false,

hide_field: false,

},

{

label: "Mobile",

value: mobile,

type: "SINGLE_LINE",

group_uid: environment.asset.customFieldsGroups.GWMSInfo.uid,

group_name: environment.asset.customFieldsGroups.GWMSInfo.name,

hide_to_fe: false,

read_only: false,

hide_field: false,

},

  

{

label: "Email",

value: email,

type: "SINGLE_LINE",

hide_to_fe: false,

group_uid: environment.asset.customFieldsGroups.GWMSInfo.uid,

group_name: environment.asset.customFieldsGroups.GWMSInfo.name,

read_only: false,

hide_field: false,

},

{

label: "Date Of Sale",

value: dateOfSale,

type: "DATE",

group_uid: environment.asset.customFieldsGroups.GWMSInfo.uid,

group_name: environment.asset.customFieldsGroups.GWMSInfo.name,

hide_to_fe: false,

read_only: false,

hide_field: false,

},

{

label: "Registration Date",

value: registrationDate,

type: "DATE",

group_uid: environment.asset.customFieldsGroups.GWMSInfo.uid,

group_name: environment.asset.customFieldsGroups.GWMSInfo.name,

hide_to_fe: false,

read_only: false,

hide_field: false,

},

{

label: "Registration Deadline",

value: registrationDeadline,

type: "DATE",

group_uid: environment.asset.customFieldsGroups.GWMSInfo.uid,

group_name: environment.asset.customFieldsGroups.GWMSInfo.name,

hide_to_fe: false,

read_only: false,

hide_field: false,

},

],

},

};
```