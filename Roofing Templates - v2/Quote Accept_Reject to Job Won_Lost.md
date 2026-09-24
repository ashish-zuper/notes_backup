
---

## Overview

This workflow synchronizes the status of an inspection job with the status of its associated quote. When a quote is accepted or rejected, the corresponding inspection job is automatically updated to "Won" or "Lost" respectively.

---

## Configurable Parameters

| Parameter            | Type      | Description                                                      | Example Value                |
|----------------------|-----------|------------------------------------------------------------------|------------------------------|
| `estimate_status`    | static    | Status of the quote that triggers the workflow                   | `APPROVED`, `DECLINED`       |
| `job_uid`            | dynamic   | UID of the associated inspection job                             | `<job_uid>`                  |
| `statusMap`          | static    | Mapping from quote status to job status                          | `{ APPROVED: 'won', DECLINED: 'lost' }` |
| `job_category`       | static    | Job category to validate before updating                         | `roof inspection`            |
| `api_key`            | static    | API key for Zuper                                                | `<API_KEY>`                  |
| `base_url`           | static    | Base URL for Zuper API                                           | `<BASE_URL>`                 |

---

## How Parameters Are Used

- **Trigger Condition:**  
  The workflow is triggered when a quote status is updated to "APPROVED" or "DECLINED" and the quote is linked to a job.

- **Job Category Validation:**  
  Only jobs with the category "roof inspection" are eligible for status updates.

- **Status Mapping:**  
  The workflow maps quote status to job status using the `statusMap` parameter.

- **API Calls:**  
  The workflow fetches job category details and job status details from Zuper before updating the job status.

---

## Process Flow

1. **Trigger:**  
   The workflow starts when a quote status is updated to "APPROVED" or "DECLINED" and the quote is linked to a job.

2. **Fetch Quote Details:**  
   Retrieves the quote and associated job details.

3. **Validate Job Category:**  
   Checks if the job category is "roof inspection".

4. **Check Current Job Status:**  
   Ensures the job is not already in the target status.

5. **Fetch Master Job Category:**  
   Retrieves job category details from Zuper.

6. **Fetch Job Statuses:**  
   Gets all statuses for the "roof inspection" category.

7. **Prepare Status Update Payload:**  
   Constructs the payload to update the job status to "Won" (if quote is approved) or "Lost" (if quote is declined).

8. **Update Job Status:**  
   Sends an API request to update the job status in Zuper.

---

## Summary

This workflow ensures that inspection jobs are automatically marked as "Won" or "Lost" based on the outcome of their associated quotes, maintaining accurate job status