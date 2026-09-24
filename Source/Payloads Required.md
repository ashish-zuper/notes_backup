
#### ticket_new
``` javascript
{
objectId:'',
event:'',
app_configs: {}
}
```

#### ticket_status_update
``` javascript
{
objectId:'',
event:'',
app_configs: {}
}
```

#### job_assign_users
``` javascript
{
job_uid:'',
event:'',
app_configs: {},
assigned_users:[],
unassigned_users:[],
triggered_by:{}
}
```

#### job_new
``` javascript
{
job_uid:'',
event:'',
job_priority:'',
parent_job:'',
app_configs: {},
assigned_users:[],
unassigned_users:[],
triggered_by:{}
}
```

#### job_schedule
``` javascript
{
job_uid:'',
event:'',
scheduled_start_time:'',
scheduled_end_time:'',
reason:'',
app_configs: {},
triggered_by:{}
}
```

#### job_status_update
``` javascript
{
job_uid:'',
event:'',
app_configs: {},
triggered_by:{}
}
```

#### job_update
``` javascript
{
job_uid:'',
event:'',
parent_job:'',
job_priority:'',
scheduled_start_time:'',
scheduled_end_time:'',
due_date:'',
child_jobs:[],
app_configs: {},
triggered_by:{}
}
```


