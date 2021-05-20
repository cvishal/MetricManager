## Predictive Insights (PI) on VM (Also referred as Metric Manager)
-----

### Introduction:
This document helps user setting up IBM Predictive Insights (PI), which is part of Cloud Pak for Watson AIOps (3.1) and integrate with Event Manager which is part of Cloud Pak for Watson AIOps.

These steps are grouped in following catagories:
- Install PI On Standalone VM on IBM Cloud VSI
- Get Required Details of OCP Based Event Manager
- Configure PI to point to OCP Based Event Manager
----

### Install Predictive Insight on IBM Cloud VSI Server.
1. [Provision VM with 4C-16GB on IBM Cloud & RHEL 7](/files/provision.md)
2. [Install all pre-reqs softwares](/files/prereq.md)
3. [Install Standalone instance of PI pointing to local object server and local LDAP](/files/installpi.md)

_Please note: You can make reusable Image Template at this moment, so its easy to share with rest of your organization for Demo or PoC Purpose_


----

### Get Watson AIOps Details (OCP based EM)
4. [Get Required Details of Event Manager on OCP](/files/ocpem.md)
5. [Add the required columns to the OCP objectservers' alerts.status tables](/files/updatetable.md)

----


### Configure PI to point to OCP Based Event Manager ()
6. [ReConfigure DASH to authenticate with remote LDAP (OCP EM)](/files/configurepi1.md)
7. [ReConfigure DASH to connect to remote Object Server.](/files/configurep2.md)
8. [Validate local WebUI connects to Remote Object Server](/files/configurepi3.md)
9. [ReConfigure PI Analytics Component to sent events to Remote Object Server](/files/configurepi4.md)
10. [ReConfigure PI Analytics UI to connect to remote LDAP](/files/configurepi5.md)

-----

##### _Note for IBM Employees_
_For Internal IBM PoC and Demo purpose, we have pre-created template, which can be leveraged. Please get in touch with cvishal@in.ibm.com or vksuktha@in.ibm.com for more details_

-----

