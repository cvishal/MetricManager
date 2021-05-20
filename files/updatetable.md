

-----
## 5. Update the OCP Based Event Manager Object Server to have addtiional Fields
-----
Login to OCP Cluster CLI, where AIOps EM is installed
The identify the Object Server pods

```
oc get pods | grep -i nco

```
Get POD names for noi-ncprimary-0 and noi-ncobackup-0 

#### Step 1:
login into nco primary 
```
oc rsh noi-ncprimary-0
once login
cd /opt/IBM/tivoli/netcool/omnibus/bin
./nco_sql -u root -p <root-pw-obj-ser> -s AGG_P
Verify that you get prompt 1>
```
#### Step 2:
Create a new file called 'conversions.sql' and add following content
```
delete from alerts.conversions where Value in (89350,89360,89370);
go
insert into alerts.conversions values ('Class89350','Class',89350,'TASP Events');
go
insert into alerts.conversions values ('Class89360','Class',89360,'TASP Consolidated Events');
go
insert into alerts.conversions values ('Class89370','Class',89370,'TASP Data Availability Events');
go
```
#### Step 3:
Run following command in rsh console

`./nco_sql -u root -p <root-pw-obj-ser> -s AGG_P < conversions.sql `
Which should be successful

Repeat Step1, 2 and 3 for noi-ncobackup-0
Use -s AGG_B in this case.


#### Step 4:
Create a new script called 'add-columns.sql' and add following lines:
```
alter table alerts.status add column TASPAlgorithmName varchar(250);
go
select TASPAlgorithmName from alerts.status where 0 = 1;
alter table alerts.status add column TASPAlgorithmInstanceName varchar(50);
go
select TASPAlgorithmInstanceName from alerts.status where 0 = 1;
alter table alerts.status add column TASPCorrelationId int;
go
select TASPCorrelationId from alerts.status where 0 = 1;
alter table alerts.status add column TASPInstanceIdentifier varchar(50);
go
select TASPInstanceIdentifier from alerts.status where 0 = 1;
alter table alerts.status add column TASPQuantifier varchar(30);
go
select TASPQuantifier from alerts.status where 0 = 1;
alter table alerts.status add column TASPUpdateTime time;
go
select TASPUpdateTime from alerts.status where 0 = 1;
alter table alerts.status add column TASPAnomalyTimestamp time;
go
select TASPAnomalyTimestamp from alerts.status where 0 = 1;
alter table alerts.status add column TASPMetricNameList varchar(500);
go
select TASPMetricNameList from alerts.status where 0 = 1;
alter table alerts.status add column TASPMetricScoreList varchar(500);
go
select TASPMetricScoreList from alerts.status where 0 = 1;
alter table alerts.status add column TASPMetricValueList varchar(500);
go
select TASPMetricValueList from alerts.status where 0 = 1;
alter table alerts.status add column TASPMetricResourceNameList varchar(500);
go
select TASPMetricResourceNameList from alerts.status where 0 = 1;
alter table alerts.status add column TASPMetricResourceTypeList varchar(500);
go
select TASPMetricResourceTypeList from alerts.status where 0 = 1;
alter table alerts.status add column TASPMetricNodeList varchar(500);
go
select TASPMetricNodeList from alerts.status where 0 = 1;
alter table alerts.status add column TASPAnomalousMetrics varchar(500);
go
select TASPAnomalousMetrics from alerts.status where 0 = 1;
alter table alerts.status add column TASPMetricGroupNameList varchar(500);
go
select TASPMetricGroupNameList from alerts.status where 0 = 1;
alter table alerts.status add column TASPAnomalousResources varchar(500);
go
select TASPAnomalousResources from alerts.status where 0 = 1;
alter table alerts.status add column TASPAnomalousMetricGroups varchar(250);
go
select TASPAnomalousMetricGroups from alerts.status where 0 = 1;
alter table alerts.status add column TASPParentIdentifier varchar(1024);
go
select TASPParentIdentifier from alerts.status where 0 = 1;
alter table alerts.status add column TASPTopic varchar(250);
go
select TASPTopic from alerts.status where 0 = 1;
alter table alerts.status add column TASPDirection varchar(50);
go
select TASPDirection from alerts.status where 0 = 1;
alter table alerts.status add column TASPRelatedID varchar(500);
go
select TASPRelatedID from alerts.status where 0 = 1;
alter table alerts.status add column TASPActualValue varchar(250);
go
select TASPActualValue from alerts.status where 0 = 1;
alter table alerts.status add column TASPExpectedValue varchar(250);
go
select TASPExpectedValue from alerts.status where 0 = 1;
alter table alerts.status add column TASPAttributeNames varchar(500);
go
select TASPAttributeNames from alerts.status where 0 = 1;
alter table alerts.status add column TASPAttributeValues varchar(500);
go
select TASPAttributeValues from alerts.status where 0 = 1;
alter table alerts.status add column TASPIdentifier varchar(1024);
go
select TASPIdentifier from alerts.status where 0 = 1;
alter table alerts.status add column TASPPriorityScore varchar(250);
go
select TASPPriorityScore from alerts.status where 0 = 1;
alter table alerts.status add column TASPAlarmNote varchar(500);
go
select TASPAlarmNote from alerts.status where 0 = 1;
go
```

Run following command in rsh console

`./nco_sql -u root -p <root-pw-obj-ser> -s AGG_P < add-columns.sql `
Which should be successful


Do the same on noi-ncobackup-0 pod as well
Use -s AGG_B in this case.
