
---

## Overview

This workflow updates the associated customer's custom field "Is Lead" to "No" when an inspection job's status is changed to "Won". It ensures that once a job is won, the customer is no longer marked as a lead in the system.

---

## Configurable Parameters

The workflow uses the following parameters and settings:

| Parameter            | Type      | Description                                                      | Example Value         |
|----------------------|-----------|------------------------------------------------------------------|----------------------|
| `customerCfLabel`    | static    | Label of the customer custom field to update                     | `Lead`               |
| `zuperApiKey`        | static    | API key for Zuper                                                | `<API_KEY>`          |
| `zuperRegion`        | static    | Base URL for Zuper API                                           | `<BASE_URL>`         |
| `custom_field_value` | static    | Value to set for the customer custom field                       | `No`                 |

---

## How Parameters Are Used

- **Trigger Condition:**  
  The workflow is triggered when a job status is updated to "Won" and the job has an associated customer.

- **Field Mapping:**  
  The workflow identifies the customer linked to the job and updates the custom field labeled "Lead" to "No".

- **API Configuration:**  
  The API key and base URL are used for authentication and communication with the Zuper API.

---

## Process Flow

1. **Trigger:**  
   The workflow starts when a job status is updated to "Won" and the job has a non-empty customer UID.

2. **Configuration:**  
   Loads configuration parameters such as API key, region, and the custom field label.

3. **Fetch Job Details:**  
   Retrieves job details to obtain the associated customer's UID.

4. **Update Customer Field:**  
   Updates the customer's custom field "Lead" to "No" using the Zuper API.

---

## Summary

This workflow automates the process of updating a customer's status from "Lead" to "No" when an inspection job is won. It helps maintain accurate customer records and ensures leads are properly converted in the