# Bootstrap and Rejoin-Unsafe Errand Issue:

<!-- @TODO https://www.pivotaltracker.com/n/projects/1968443/stories/141294911 -->

### Table of Contents
- [Symptoms](# Symptoms)
- [Triage (Required)](#triage)
- [Procedure](#procedure)
  - [Install the UAA CLI and authenticate](#bootsrap-mysql)
  - [Validate MySQL password](#validate-mysql-password)
- [Resources](#resources)

## Symptoms
There is an issue in versions 1.8.0 - 1.8.2 in which the bootstrap and rejoin-unsafe errands fail with an error like this:
```
Error 100: Unable to render jobs for instance group 'rejoin-unsafe'. Errors are:
   - Unable to render templates for job 'rejoin-unsafe'. Errors are:
     - Error filling in template 'config.yml.erb' (line 8: Can't find link 'arbitrator')
     
```
This is a bug in those releases. It will be addressed in a coming release.

## Triage (Required)

 Complete the required triage for MySQL

## Procedure
 Follow these steps to avoid the issue:

For **bootstrapping**, you must use the manual bootstrap instructions to restore access to the cluster.:
  - [ ] [MySQL 1.9](http://docs.pivotal.io/p-mysql/1-9/bootstrapping.html#manual-bootstrap)
  - [ ] [MySQL 1.8](http://docs.pivotal.io/p-mysql/1-8/bootstrapping.html#manual-bootstrap)
  - [ ] [MySQL 1.7](http://docs.pivotal.io/p-mysql/1-7/bootstrapping.html#manual-bootstrap)

For **rejoin-unsafe**, you must follow these steps:
- [ ] Log into the node which has tripped the interruptor and become root.
- [ ] Stop mariadb_ctrl 
```
monit stop mariadb_ctrl
```
- [ ] Remove the mysql directory from the persistent disk
```
rm -rf /var/vcap/store/mysql
```
- [ ] Run the pre-start script
```
/var/vcap/jobs/mysql/bin/pre-start
```
- [ ] Start mariadb_ctrl
```
monit start mariadb_ctrl
```


 

## Resources
For step by step details check the [Prerequisites](#prerequisites) section above.

















###### [Runbooks](../Runbook.md)
