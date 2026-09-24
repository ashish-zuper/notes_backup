execution_history_data : 12927847
node_executions_archive: 2152026
workflow_executions: 3250882
workflow_executions_archive: 611189

March 28 5 55
workflow_executions_archive: 148407
node_executions_archive: 620298



April  6
### Archive (executions older than retention, not yet archived):   

```
SELECT COUNT(*) FROM workflow_executions                                         
  WHERE archival_status IS NULL                                                  
  AND created_at < DATE_SUB(NOW(), INTERVAL 90 DAY); 
```
299519
April 16: 345009
### S3 Migration (executions needing S3 migration):

```                                                                                                                      
  SELECT COUNT(*) FROM workflow_executions
  WHERE s3_migration_needed = 1
  AND status IN ('COMPLETED', 'FAILED', 'SKIPPED');     
```

1851885

April 8 : 484453
April: 16  17309
```
SELECT COUNT(*) FROM execution_history_data                                      
  WHERE s3_migration_needed = 1                                                  
  AND status IN ('COMPLETED', 'FAILED', 'SKIPPED');  
```
1,20,43,743
1,19,41,370
1,20,04,992

### Clear Skipped (skipped executions older than retention):

```
  SELECT COUNT(*) FROM workflow_executions
  WHERE status = 'SKIPPED'                
  AND created_at < DATE_SUB(NOW(), INTERVAL 10 DAY);     
```

### Clear Expired Test (expired webhook test records):          
```
SELECT COUNT(*) FROM webhook_test_executions                                   
  WHERE created_at <= DATE_SUB(NOW(), INTERVAL 30 MINUTE);  
```       
  
45093
### Archive Tables (legacy rows pending migration):                                

```
 SELECT COUNT(*) FROM workflow_executions_archive;                              
  SELECT COUNT(*) FROM node_executions_archive;  
```
 0