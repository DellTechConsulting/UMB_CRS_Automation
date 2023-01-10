## UMB-CRS Automation
### Automate CRS Replication 
### This is an ansible template for a replication usecase, in which we use tags such as get, add, create, and lock.
get and add tags is used to get the details of policy,copy  and mapping the policy name to policy id , 
scan - used to analyze the copy and scanstatus is used to check the status of scan job, analysisstatus is used to find the good copy and recover tag used to recover the good copy.

![image](https://user-images.githubusercontent.com/94111270/207880273-92ddf03d-0225-4cd6-8682-de4fc6767bff.png)


## Below is a picture of the variable used in ansible tower.
![image](https://user-images.githubusercontent.com/94111270/207880988-57755172-2c7f-4ba1-82e9-335aa1a593e8.png)

## This is the success ful job template in ansible tower .
![image](https://user-images.githubusercontent.com/94111270/207881953-3eb1c1c3-2692-4228-b250-8fa39aefdf4f.png)

## using Anisble roles executing the automate_avamar_recovery playbook 
#### These are the playbooks associated with the roles 
   1 Policy_validation.yml
   2 copy_id.yml
   3 copy_scan.yml
   4 copy_scan_status_check.yml
   5 analyze_details.yml
   6 delete.yml
   7 recovery.yml

#### Policy_validation.yml performing the below tasks 
Task 1- Get CRS API authentication token
Task 2 - Get all CR Policy details 
Task-3 - Fetching the policy names from the policy details
policy_name: ['CNWLinux1','CRS-RDC-LAB-NWSRV1','AVE','CRS_Test','CRS-RDC-LAB-NWSRV3','TEST_NEW']
Task 4- validating the passing policy name exist/not
   Sub task 4.1 printing policy name exist
   Sub task 4.2 Failing the playbook scinc epolicy name  does not exist
Task 5 mapping the policy name with policy id
end of the playbook by passing the policy name in variable file , we are fecthing the corresponding policy id, that id is used to do the replication.

### copy_id.yml performs the below tasks.

Task 1- Get CRS API authentication token
Task 2 - Get all CR copy details of each policy
Task-3 - Failing the playbook if there are no copies found
Task-4 - fetching the point in time copy in each policy based on creationdate
Task-5 - fecthing the copy id from the copy details
### copy_scan.yml performs below tasks.
Task 1 -scan the point in time copy using copy id 
### copy_scan_status_check.yml performs the below tasks.
Task 1- It is checking the status of the scan job untill it succeed 
### analyze_details.yml performs below tasks.
this tasks check whether the copy is good/ having any issue .

### recover.yml 
if the copy is good then its recover and restore using avamar. 

## How to run in Postman

The image below shows a sample postman request:

<img width="629" alt="Capture1" src="https://user-images.githubusercontent.com/94111270/204519699-5dce2061-4ac5-496f-afba-36a1dd72d2e8.PNG">
