# UMB-CRS Automation
## Automate CRS Replication 
## Excecute the crs_replication playbook 
# using Anisble roles executing the playbook 
# under the roles we have these are the playbooks 
   1 Policy_validation.yml
   2 replication.yml
   3 check_job_status.yml
   4 copy_lock.yml
   5 check_lock_status.yml
   6 main.yml

## Policy_validation.yml performing the below tasks 
Task 1- Get CRS API authentication token
Task 2 - Get all CR Policy details 
Task-3 - Fetching the policy names from the policy details
# policy_name: ['CNWLinux1','CRS-RDC-LAB-NWSRV1','AVE','CRS_Test','CRS-RDC-LAB-NWSRV3','TEST_NEW']
Task 4- validating the passing policy name exist/not
   Sub task 4.1 printing policy name exist
   Sub task 4.2 Failing the playbook scinc epolicy name  does not exist
Task 5 mapping the policy name with policy id
# end of the playbook by passing the policy name in variable file , we are fecthing the corresponding policy id, that id is used to do the replication.


## replication.yml performs the below tasks.

Task 1 - create replication of the Policy ,using the the above policy id. [policy id is registed in id variable]
# From this task ,we will obtain a Job id, using that job id we are checking the job status.
# that job id is regestered in jid variable.


## Check_job_status.yml performs below tasks.
Task 1 -Check the status of the Job
Task 2 -Get CRS API authentication token
Task 3 -Get the job status
# will check the status until job(Replication) get sucess.
Task 4 pause  (here giving a pause time of 10 min because it requires some time to comeplete the job )

## copy_validation.yml performs the below tasks.
Task 1- Get the job status using jid 
Task 2 -printing copy status with copy id 
# after completiom of replication , will obtain a copy id [registerd in cid variable].
# we can cross check in GUI from the corresponding copy id.

## copy_lock.yml performs below tasks.
Task 1 -Get copy details using copy id and policy id
 [In that details , we will check the copy status (lock/unlock) if copy has been already locked ,fail the playbook, if copy is unlock then its going to perform the lock action]

## check lock status.yml 
In this task, we are keep on checking the job status untill the job get success. 
Once its success , it display the success message. 

## How to run in Tower

The image below shows how to run the job template in ansible tower:
<img width="744" alt="TowerRun" src="https://user-images.githubusercontent.com/94111270/204515676-34150d15-2525-4868-8970-e058c3c27434.PNG">

## How to run in Postman

The image below shows a sample postman request:


<img width="629" alt="Capture1" src="https://user-images.githubusercontent.com/94111270/204519699-5dce2061-4ac5-496f-afba-36a1dd72d2e8.PNG">
