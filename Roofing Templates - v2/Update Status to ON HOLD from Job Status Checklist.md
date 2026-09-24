
---

## Overview

This workflow automatically updates a job's status to "ON HOLD" if a specific checklist question is answered "Yes" during a job status update. It helps ensure that jobs requiring attention or materials are flagged and paused until resolved.

---

## Configurable Parameters

The workflow uses the following parameters and settings:

| Parameter                   | Type      | Description                                                      | Example Value                        |
|-----------------------------|-----------|------------------------------------------------------------------|--------------------------------------|
| `zwb_chj_checklist_question`| static    | The checklist question to monitor                                | `"Do you have all materials needed for the job?"` |
| `job_status_name`           | static    | Name for the "ON HOLD" status                                    | `"On Hold"`                          |

---

## How Parameters Are Used

- **Checklist Monitoring:**  
  The workflow checks the value of the specified checklist question when a job status update occurs.

- **Conditional Logic:**  
  If the answer to the checklist question is "Yes", the workflow proceeds to update the job status to "ON HOLD". Otherwise, no action is taken.

- **Job Status Update:**  
  The workflow uses the provided job status UID and name to set the job to "ON HOLD" via the Zuper API.

---

## Process Flow

1. **Trigger:**  
   The workflow starts when a job status is updated to a specific status (e.g., "Site Preparation").

2. **Checklist Value Extraction:**  
   Retrieves the value of the target checklist question from the job status update payload.

3. **Condition Check:**  
   Uses an If/Else node to check if the checklist answer is "Yes".

4. **Status Update:**  
   - If "Yes": Updates the job status to "ON HOLD" using the Zuper API.
   - If not "Yes": No operation is performed.

---

## Summary

This workflow ensures that jobs are automatically put on hold if a critical checklist item (such as missing materials) is flagged during a status update. It helps prevent jobs from progressing without necessary resources