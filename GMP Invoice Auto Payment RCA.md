
Workflow 1: https://internalwf.zuper.co/workflow/Wsdp0xOjhNtoMDwq/executions/67057361

Process:
- Cron runs daily at 9pm CDT
- Fetch all invoices with due date = TODAY and status = AWAIT_PAYMENT
- Get all customers associated to each invoice
- Check if there are any customers with auto charge enabled and have auto charge card on file
- If none found stop execution
- Else charge customer for each invoice with total invoice amount


Workflow 2: https://internalwf.zuper.co/workflow/kM0f120llNlQF1Ui

Process:
- Cron runs daily CDT
- Fetch all invoices with invoice date = TODAY 
- If custom field: Send Invoices Automatically is set as Yes, send to customer and update status to AWAIT_PAYMENT



RCA:
- If both the due date and invoice dates are on the same day, both the above workflows will run at the same time. 
- So in workflow 1, the invoice will not be fetched since the workflow 2 has not updated the status to AWAIT_PAYMENT 
- Since status was not equal to : AWAIT_PAYMENT during the time of workflow 1, the invoice did not proceed for auto payment

Solution:
- Need to change the trigger time of workflow 2 to less than 9pm CDT
- Thus we can ensure that both the workflows will never be executed at the same time


INVOICE: 2150
- Due Date : 07/25/2025
- Invoice Date: 07/25/2025
- Status of Invoice on 07/25/2025  :  DRAFT
- ![[Pasted image 20250805143639.png]]

INVOICE: 1776
- Due Date: 07/25/2025
- Invoice Date: 07/25/2025
- Status of Invoice on 07/25/2025  :  DRAFT
- ![[Pasted image 20250805150226.png]]

INVOICE: 2675
- Due Date: 07/25/2025
- Invoice Date: 07/25/2025
- Status of Invoice on 07/25/2025  :  DRAFT
- ![[Pasted image 20250805145909.png]]
