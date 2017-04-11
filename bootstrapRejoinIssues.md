# Bootstrap and Rejoin-Unsafe Errand Issue:

<!-- @TODO https://www.pivotaltracker.com/n/projects/1968443/stories/141294911 -->

### Table of Contents
- [Symptoms](#Symptoms)
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

## Triage (Required)

 Complete the required triage for MySQL

## Procedure
This is a bug in those releases. It will be addressed in a coming release. In the meanwhile, it may be necessary to perform these steps manually:

For bootstrapping, you must use the manual bootstrap instructions to restore access to the cluster.:
  - [ ] [MySQL 1.9](http://docs.pivotal.io/p-mysql/1-9/bootstrapping.html#manual-bootstrap)
  - [ ] [MySQL 1.8](http://docs.pivotal.io/p-mysql/1-8/bootstrapping.html#manual-bootstrap)
  - [ ] [MySQL 1.7](http://docs.pivotal.io/p-mysql/1-7/bootstrapping.html#manual-bootstrap)



For rejoin-unsafe, you must follow these steps:
Log into the node which has tripped the interruptor and become root.
monit stop mariadb_ctrl
rm -rf /var/vcap/store/mysql
/var/vcap/jobs/mysql/bin/pre-start
monit start mariadb_ctrl





The service plan you expect to exist is no longer available. If and only if the Operator does all of these steps in sequence, a plan will become “unrecoverable”:
  1. Click the trash-can icon in the Service Plan screen
  2. Enter a plan with the exact same name
  3. Click the ‘Save’ button on the same screen
  4. Return to the Ops Manager top-level, and click 'Apply Changes’
After clicking 'Apply Changes’, the deploy will eventually fail with the error:
```
Server error, status code: 502, error code: 270012, message: Service broker catalog is invalid: Plan names must be unique within a service
```

## Procedure

### Triage (Required)
  - [ ] If you have committed steps 1 and 2, but not 4, no problem. Do not hit the 'Save’ button. Simply return to the Installation Dashboard. Any accidental changes will be discarded.
  - [ ] If you have committed steps 1, 2 and 3, do not click 'Apply Changes.’ Instead, return to the Installation Dashboard and click the ’Revert’ button. Any accidental changes will be discarded.
  

## Resources
For step by step details check the [Prerequisites](#prerequisites) section above.

















###### [Runbooks](../Runbook.md)
