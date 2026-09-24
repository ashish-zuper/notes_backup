
---

## Overview

This workflow automatically creates a purchase order (PO) for the line items in an Install/Replace job when the job is created and has a parent inspection job attached. It ensures that all required materials and services are ordered promptly for installation jobs.

---

## Configurable Parameters

| Parameter            | Type      | Description                                                      | Example Value                |
|----------------------|-----------|------------------------------------------------------------------|------------------------------|
| `parent_job`         | dynamic   | Parent job UID must be present                                   | `<inspection_job_uid>`       |
| `po_template`        | static    | PO template name to use                                          | `Default Template`           |
| `po_payment_term`    | static    | Payment term for PO                                              | `Immediate`                  |
| `po_required_by`     | dynamic   | Required by date for PO (from job due date)                      | `due_date`                   |
| `zuper_api_key`      | static    | API key for Zuper                                                | `<API_KEY>`                  |
| `zuper_base_url`     | static    | Base URL for Zuper API                                           | `<BASE_URL>`                 |
| `timezone`           | static    | Timezone for date formatting                                     | `<ZUPER_COMPANY_TIMEZONE>`   |

---

## How Parameters Are Used

- **Trigger Condition:**  
  The workflow is triggered when a new job is created with category "Install/Replace" with a parent job is attached.

- **Field Mapping:**  
  PO template, payment term, and required by date are mapped from static or dynamic values in the job.

- **Product Extraction:**  
  All products (line items) from the job are extracted and grouped by vendor.

- **Vendor Catalog Population:**  
  Vendor details and SKUs are fetched for each product to build the PO.

- **PO Payload Construction:**  
  The workflow builds a PO payload for each vendor, including job details, shipping address, template, payment term, due date, and line items.

- **API Calls:**  
  The workflow makes HTTP requests to fetch payment terms, templates, product details, and finally creates the PO in Zuper.

---

## Process Flow

1. **Trigger:**  
   The workflow starts when a new Install/Replace job is created with a parent inspection job.

2. **Settings Initialization:**  
   Loads workflow settings and field mappings.

3. **Fetch Job Details:**  
   Retrieves job details, including products and customer address.

4. **Fetch Payment Terms & Templates:**  
   Gets available payment terms and PO templates from Zuper.

5. **Extract Product UIDs:**  
   Collects product UIDs from job line items.

6. **Fetch Product Details:**  
   Retrieves product and vendor catalog details for each product.

7. **Build PO Payload:**  
   Groups products by vendor and constructs a PO payload for each vendor.

8. **Create Purchase Order:**  
   Sends a bulk API request to create purchase orders for all vendors involved.

9. **Error Handling:**  
   If no products or vendors are found, the workflow stops and returns an error message.

---

## Summary

This workflow streamlines the procurement process for installation jobs by automatically generating purchase orders for all required materials and services, grouped by vendor, as soon as the job is created. It reduces manual effort and ensures timely ordering for job