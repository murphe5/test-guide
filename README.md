# Scaling Down MySQL Runbook:

<!-- @TODO https://www.pivotaltracker.com/story/show/141213893  -->

### Table of Contents
- [Prerequisites](#prerequisites)
- [Check the Health of Your Cluster](http://docs.pivotal.io/p-mysql/1-8/scaling-down.html#check-health)
- [Scale down your cluster](http://docs.pivotal.io/p-mysql/1-8/scaling-down.html#scale-down)
  

## Prerequisites
- [ ] Before scaling down your MySQL cluster, perform the following actions to ensure the cluster is healthy.:
  - [ ] [MySQL 1.9](http://docs.pivotal.io/p-mysql/1-9/mysql-diag.html#healthy)
  - [ ] [MySQL 1.8](http://docs.pivotal.io/p-mysql/1-8/scaling-down.html#check-health)
  - [ ] [MySQL 1.7](http://docs.pivotal.io/p-mysql/1-7/scaling-down.html#check-health)

## Procedure

### Triage (Required)
  - [ ] Complete the required [triage for MySQL](../README.md#triage-required)
  
### Scale down your cluster
- [ ] Delete the dummy database. When prompted for a password, provide the password value obtained above.
```
$ mysql -h FIRST-NODE-IP-ADDRESS -u YOUR-IDENTITY -p -e "drop database verify_healthy;"
```
- [ ] From the PCF **Installation Dashboard**, click the **MySQL for Pivotal Cloud Foundry** tile.

- [ ] Click the **Settings** tab.

- [ ] Click **Resource Config** and use the drop-down menu to change the Instances count for **MySQL Server** to **1**.

- [ ] Click **Save** to apply the changes.


###### [Runbooks](../Runbook.md)
