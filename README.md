# Scaling Down MySQL Runbook:

### @TODO https://www.pivotaltracker.com/story/show/141213893

### Table of Contents
- [Prerequisites](#prerequisites)
- [Check the Health of Your Cluster](#Check the Health of Your Cluster)
- [Scale down your cluster](#http://docs.pivotal.io/p-mysql/1-8/scaling-down.html#scale-down)
  

## Prerequisites
- [ ] To rotate MySQL credentials please read the following:
  - [ ] [MySQL 1.9](http://docs.pivotal.io/p-mysql/1-9/credential-rotation.html)
  - [ ] [MySQL 1.8](http://docs.pivotal.io/p-mysql/1-8/credential-rotation.html)
  - [ ] [MySQL 1.7](http://docs.pivotal.io/p-mysql/1-7/credential-rotation.html)

## Symptoms

When to execture this? @TODO

## Procedure

### Triage (Required)
  - [ ] Complete the required [traige for MySQL](../README.md#triage-required)
  
### Install the UAA CLI and authenticate
- [ ] Install UAA CLI
```
gem install cf-uaac
```
- [ ] Check UAA is installed
```
which uaac
```
- [ ] Target Ops Manager UAA
```
uaac target https://YOUR-OPSMAN-FQDN/uaa/ --ca-cert YOUR-ROOT-CA.crt 
```
- [ ] Get token with Client ID set to opsman, Client secret leave blank, username & password are the same as logging into ops man admin GUI
```
uaac token owner get
```
- [ ] Display context
```
uaac context
```
- [ ] Create a file called `uaac-token`
- [ ] Add the value from uaac context output for the value `access_token`
- [ ] Use curl to call Ops Manager API amd pipe to file
```
curl -skH "Authorization: Bearer $(cat uaac-token)" https://YOUR-OPSMAN-FQDN/api/installation_settings > \
installation_settings_current.json
```
### Validate MySQL password

- [ ] Check MySQL root password in current installtion file
```
grep -c YOUR-MYSQL-FOR-PCF-ROOT-PASSWORD installation_settings_current.json
```
- [ ] (optional) If you use Elastic Runtime MySQL, you should also run the following command
```
 grep -c YOUR-ERT-MYSQL-ROOT-PASSWORD installation_settings_current.json
```
- [ ] Remove the root password
```
sed -e's/"value":{"identity":"root","password":"[^"]*"},\("identifier":"mysql_admin\)/\1/g' \ 
installation_settings_current.json > installation_settings_updated.json
```
- [ ] Check root password has been removed
```
grep -c YOUR-MYSQL-FOR-PCF-ROOT-PASSWORD installation_settings_updated.json
```
- [ ] (optional) If you use Elastic Runtime MySQL, you should also run the following command
```
grep -c YOUR-ERT-MYSQL-ROOT-PASSWORD installation_settings_updated.json
```

### Upload the updated installation settings

- [ ] Upload the updated installation settings
```
curl -skX POST -H "Authorization: Bearer $(cat uaac-token)" "https://YOUR-OPSMAN-FQDN/uaa/api/installation_settings" \
-F 'installation[file]=@installation_settings_updated.json'
```
- [ ] Navigate to the Ops Manager Installation Dashboard and click `Apply Changes`
- [ ] Once the installation has completed, validate that the MySQL for PCF root password has been changed
```
mysql -uroot -p -h 198.51.100.1
```
- [ ] (optional) If you use Elastic Runtime MySQL, you should also validate that the Elastic Runtime MySQL root password has been changed

## Resources
For step by step details check the [Prerequisites](#Prerequisites) section above.



###### [Runbooks](../Runbook.md)














###### [Runbooks](../Runbook.md)
