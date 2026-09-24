	
---

## Overview

This workflow automatically updates the status of a job to "Invoiced" when a new invoice is created and linked to that job. It ensures that jobs are properly tracked and marked as invoiced in the system as soon as billing occurs.

---

## Configurable Parameters

The workflow uses the following parameters and settings:

| Parameter            | Type      | Description                                                      | Example Value                        |
|----------------------|-----------|------------------------------------------------------------------|--------------------------------------|
| `job_status_name`    | static    | Name for the "Invoiced" status                                   | `Invoiced`                           |

---

## How Parameters Are Used

- **Trigger Condition:**  
  The workflow is triggered when a new invoice is created and linked to a job.

- **Job Identification:**  
  The job UID is extracted from the invoice details to identify which job to update.

- **Conditional Logic:**  
  The workflow checks if the job category is "Repair Service" before updating the status.

- **Job Status Update:**  
  The job status is set to "Invoiced" using the provided status UID and name via the Zuper API.

---

## Process Flow

1. **Trigger:**  
   The workflow starts when a new invoice is created and contains a valid job UID.

2. **Fetch Invoice Details:**  
   Retrieves the invoice details, including the associated job and its category.

3. **Condition Check:**  
   Uses an If/Else node to check if the job category is "Repair Service".

4. **Status Update:**  
   - If the job category is "Repair Service": Updates the job status to "Invoiced".
   - If not: No action is performed.

---

## Summary

This workflow automates the process of marking jobs as invoiced when billing occurs, specifically for repair service jobs. It helps maintain accurate job status records and streamlines the invoicing