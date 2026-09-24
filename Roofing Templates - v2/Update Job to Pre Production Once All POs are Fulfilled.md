
---

## Overview

This workflow automatically updates the status of a job to "Pre Production" once all associated purchase orders (POs) are marked as "Fulfilled". It ensures that jobs only move to the pre-production phase when all required materials and services have been received.

---

## Configurable Parameters

| Parameter            | Type      | Description                                                      | Example Value                |
|----------------------|-----------|------------------------------------------------------------------|------------------------------|
| `zuper_api_key`      | static    | API key for Zuper                                                | `<API_KEY>`                  |
| `zuper_base_url`     | static    | Base URL for Zuper API                                           | `<BASE_URL>`                 |
| `timezone`           | static    | Timezone for date formatting                                     | `<ZUPER_COMPANY_TIMEZONE>`   |
| `trigger_status`     | static    | PO status that triggers workflow                                 | `FULFILLED`                  |
| `job_status_name`    | static    | Name for the "Pre Production" status                             | `Pre Production`             |

---

## How Parameters Are Used

- **Trigger Condition:**  
  The workflow is triggered by a webhook event when a PO status is updated.

- **PO Details Fetch:**  
  Retrieves details of the updated PO, including its status and associated job.

- **Validation:**  
  Checks if the PO status is "FULFILLED" and if the PO is linked to a job.

- **Open PO Check:**  
  Filters all POs for the job to ensure no open (unfulfilled) POs remain.

- **Job Status Update:**  
  If all POs are fulfilled, updates the job status to "Pre Production" using the provided status UID and name.

---

## Process Flow

1. **Trigger:**  
   The workflow starts when a PO status update webhook event is received.

2. **Settings Initialization:**  
   Loads workflow settings including API key, base URL, and trigger status.

3. **Fetch PO Details:**  
   Retrieves the details of the updated PO and its associated job.

4. **Validation:**  
   Checks if the PO status is "FULFILLED" and if the PO is linked to a job.

5. **Filter Open POs:**  
   Builds a payload to filter and fetch all open (unfulfilled) POs for the job.

6. **Fetch All Open POs:**  
   Makes an API call to get all open POs for the job.

7. **Check for Remaining Open POs:**  
   If no open POs are found, proceeds to update the job status.

8. **Update Job Status:**  
   Updates the job status to "Pre Production" using the Zuper API.

---

## Summary

This workflow ensures jobs only move to the pre-production phase after all purchase orders are fulfilled, improving operational accuracy