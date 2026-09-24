
---

## Overview

This workflow automates the creation of an installation job (as a child job) when an inspection job is marked as "Won". It copies relevant data, attachments, and custom fields from the parent job and/or approved quote, based on configurable parameters.

---

## Configurable Parameters

The workflow uses a settings object to control its behavior. Key configurable parameters include:

| Parameter              | Type      | Description                                                                 | Example Value                |
|------------------------|-----------|-----------------------------------------------------------------------------|------------------------------|
| `job_due_date_buffer`  | static    | Number of buffer days to add to the triggered date for new job due date      | `3`                          |
| `job_category`         | static    | Category for the new job                                                     | `Install/Replace`            |
| `copy_line_items`      | static    | Whether to copy line items from parent job                                   | `yes` / `no`                 |
| `copy_attachments`     | static    | Whether to copy attachments from parent job                                  | `yes` / `no`                 |
| `inspection_job_card`  | static    | Title of the inspection job card to attach                                   | `Inspection Job Card AI`     |
| `create_as_child_job`  | static    | Whether to create the new job as a child job                                 | `yes` / `no`                 |
| `copy_custom_fields`   | static    | Whether to copy custom fields from parent job                                | `yes` / `no`                 |
| `job_title`            | dynamic   | Title for the new job, can use dynamic values                                | `$job_category, job_title`   |
| `zuper_api_key`        | static    | API key for Zuper                                                            | `<API_KEY>`                  |
| `zuper_base_url`       | static    | Base URL for Zuper API                                                       | `<BASE_URL>`                 |
| `timezone`             | static    | Timezone for date calculations                                               | `<ZUPER_COMPANY_TIMEZONE>`   |

---

## How Parameters Are Used

- **Field Mapping:**  
  Parameters define how fields are mapped from the parent job or quote to the new job (static, dynamic, or custom).

- **Job Creation:**  
  Settings control what data is copied, how the job is titled, and whether it is created as a child job.

- **API Configuration:**  
  API key, base URL, and timezone are used for all Zuper API interactions.

- **Conditional Logic:**  
  Parameters like `copy_line_items`, `copy_attachments`, and `copy_custom_fields` determine if respective data is transferred.

---

## Process Flow

1. **Trigger:**  
   - Workflow starts when the Inspection job status is updated to "Won".

2. **Fetch Data:**  
   - Retrieves job record, job custom fields, job category, and job card templates.

3. **Settings Initialization:**  
   - Loads settings and field mappings.

4. **Conditional Checks:**  
   - Determines if job card and quote data should be attached/copied.

5. **Quote & Attachment Handling:**  
   - Fetches approved quote details and uploads templates/attachments to S3 if required.

6. **Payload Construction:**  
   - Builds the payload for the new job using settings, job details, quote line items, custom fields, and attachments.

7. **Job Creation:**  
   - Sends an HTTP POST request to Zuper to create the new installation job.
   - Handles errors and stops workflow if job creation fails.

---

## Summary

This workflow streamlines the post-inspection process by automatically creating a child installation job with all necessary data, based on configurable parameters. It ensures consistency, reduces manual effort, and supports flexible customization for different business needs.
