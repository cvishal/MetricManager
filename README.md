# Predictive Insights (PI) on VM (Part of Cloud Pak for Watson AIOps also referred as  as Metric Manager)

---- 
## Setup standalone PI Instance

These steps are grouped in following catagories:
- Install PI On Standalone VM on IBM Cloud VSI
- Get Required Details of OCP Based Event Manager
- Configure PI to point to OCP Based Event Manager
----

### Install Predictive Insight on IBM Cloud VSI Server.
1. [Provision VM with 4C-16GB on IBM Cloud & RHEL 7](/files/provision.md)
2. [Install all pre-reqs softwares](/files/prereq.md)
3. [Install Standalone instance of PI pointing to local object server and local LDAP](/files/installpi.md)

*_Please note: You can make Image Template at this moment, so its easy to share with rest of your organization_*
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

_For Internal IBM, we have already created template, which can be leveraged for PI Setup on IBM Cloud. Please get in touch with cvishal@in.ibm.com or vksuktha@in.ibm.com for more details_

-----
