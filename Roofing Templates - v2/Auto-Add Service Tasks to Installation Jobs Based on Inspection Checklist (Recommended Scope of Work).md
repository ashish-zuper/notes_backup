
---

## Overview

This workflow automatically adds a set of predefined service tasks to installation jobs when the parent inspection job's checklist indicates "replacement" or "repair" as the recommended action. It ensures that installation jobs are properly scoped and scheduled based on inspection findings.

---

## Configurable Parameters

The workflow uses the following parameters and settings:

| Parameter                        | Type      | Description                                                      | Example Value                |
|-----------------------------------|-----------|------------------------------------------------------------------|------------------------------|
| `inspectionCompletedStatusName`   | static    | Status name in parent job indicating inspection completion        | `"inspection report"`        |
| `scopeOfWorkChecklistName`        | static    | Checklist question to check for recommended scope of work         | `"recommended scope of work"`|
| `allowedChecklistAnswers`         | static    | Valid answers to trigger service task addition                    | `["replacement", "repair"]` |
| `service_task`                    | static    | List of service tasks to add to the job                           | See below                    |

---

## How Parameters Are Used

- **Trigger Condition:**  
  The workflow is triggered when a new job is created with category "Install/Replace" and has a parent job.

- **Checklist Validation:**  
  The workflow fetches the parent job's details and checks the answer to the "recommended scope of work" checklist question in the "inspection report" status.

- **Conditional Logic:**  
  If the checklist answer is "replacement" or "scope of work", the workflow proceeds to add the predefined service tasks to the installation job.

- **Service Task Addition:**  
  The workflow uses the provided list of service tasks and adds them to the job using the Zuper API.

---

## Service Tasks Added

| Checklist Answer   | Service Tasks Added                                                                                                                                                                                                 |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `replacement`      | - Tear-Off (Removal of Old Roof)<br>- Decking Inspection & Repair<br>- Underlayment Installation<br>- Flashing Installation<br>- Shingle or Roofing Material Installation<br>- Roof Penetration Sealing<br>- Ventilation Installation<br>- Final Sealing & Detailing<br>- Cleanup & Waste Disposal<br>- Final Inspection |
| `repair`    | - Site Preparation<br>- Tear-Off (Removal of Old Roof)<br>- Decking Inspection & Repair<br>- Underlayment Installation<br>- Flashing Installation<br>- Shingle or Roofing Material Installation<br>- Roof Penetration Sealing<br>- Ventilation Installation<br>- Final Sealing & Detailing<br>- Cleanup & Waste Disposal<br>- Final Inspection |

---

## Process Flow

1. **Trigger:**  
   The workflow starts when a new installation job is created with a parent job.

2. **Configuration:**  
   Loads configuration parameters for status and checklist names.

3. **Fetch Job Details:**  
   Retrieves the current job and its parent job details.

4. **Checklist Validation:**  
   Checks the parent job's "inspection report" status for the "recommended scope of work" checklist answer.

5. **Condition Check:**  
   - If the answer is "replacement": Adds the "replacement" service tasks.
   - If the answer is "repair": Adds the "repair" service tasks.
   - Otherwise: No operation is performed.

6. **Service Task Addition:**  
   Adds the relevant service tasks to the installation job.

---

## Summary

This workflow automates the process of scoping installation jobs based on inspection results. By checking the recommended scope of work in the parent inspection job, it ensures that all necessary service tasks are scheduled, improving