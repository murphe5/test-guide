# Scaling Down MySQL Runbook:

### @TODO https://www.pivotaltracker.com/story/show/141213893

### Table of Contents
- [Prerequisites](#prerequisites)
- [Check the Health of Your Cluster](#http://docs.pivotal.io/p-mysql/1-8/scaling-down.html#check-health)
- [Scale down your cluster](#http://docs.pivotal.io/p-mysql/1-8/scaling-down.html#scale-down)
  

## Prerequisites
- [ ] Before scaling down your MySQL cluster, perform the following actions to ensure the cluster is healthy.:
  - [ ] [MySQL 1.9](http://docs.pivotal.io/p-mysql/1-9/mysql-diag.html)
  - [ ] [MySQL 1.8](http://docs.pivotal.io/p-mysql/1-8/scaling-down.html#check-health)
  - [ ] [MySQL 1.7](http://docs.pivotal.io/p-mysql/1-7/scaling-down.html#check-health)

## Symptoms

When to execture this? @TODO

## Procedure

### Triage (Required)
  - [ ] Complete the required [triage for MySQL](../README.md#triage-required)
  
### Delete the dummy database 
- [ ] Replace FIRST-NODE-IP-ADDRESS with the IP address of the first MySQL server node and YOUR-IDENTITY with the identity value obtained above. When prompted for a password, provide the password value obtained above.
```
$ mysql -h FIRST-NODE-IP-ADDRESS -u YOUR-IDENTITY -p -e "drop database verify_healthy;"
```
- [ ] From the PCF Installation Dashboard, click the MySQL for Pivotal Cloud Foundry tile.

- [ ] Click the Settings tab.

- [ ] Click Resource Config and use the drop-down menu to change the Instances count for MySQL Server to 1.

- [ ] Click Save to apply the changes.


## Resources
For step by step details check the [Prerequisites](#Prerequisites) section above.



###### [Runbooks](../Runbook.md)
