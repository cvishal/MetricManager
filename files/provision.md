
# Getting Started with Predictive Insight Installation.


----
## 1. Provision VM with 4C-16GB on IBM Cloud & RHEL 7
----
In this scenario </br>
`IP : 150.238.97.xxxx` </br>
`Hostname: pi-demo.Hybrid-Squad.cloud` </br>
`Hostname -f : pi-demo` </br>

`yum update`

Install VNCServer on this VM

```
yum groupinstall "GNOME Desktop"
OR
yum groupinstall gnome-desktop
yum install xterm
yum install tigervnc-server xorg-x11-fonts-Type1
cp /lib/systemd/system/vncserver@.service /etc/systemd/system/vncserver@:3.service
vncserver :3 
```
- Setup the password, first time.
Go to vncviewer and login with ip:3, followed by password.


-----
###  Prep for installtion 

#### Step 1:
Create required users and groups
https://www.ibm.com/support/knowledgecenter/en/SSJQQ3_1.3.6/com.ibm.scapi.doc/install_guide/t_scapi_addtherequiredusers.html


#### Step 2:
Get all required installables from PartnerWorld Software Access Catalog or passport advatage:
- Go to following link </br>
- https://www.ibm.com/partnerworld/program/benefits/software-access-catalog
- Search for "Predictive Insights" and select v1.3.6 eAssembly.

- Get https://www.ibm.com/support/pages/node/737599

##### Get the PI Installables
- Select CJ36TEN assembly and download all the images to this new VM.

#### List of installables on your systems
- IBM Operations Analytics Predictive Insights Managed Device based v1.3.6 Multiplatform English (CNJ9LEN)
- IBM Streams V4.2.0.3 for RHEL7 x86 64 bit English Image (CNH5LEN )
- IBM Db2 Server V11.5.4 for Linux on AMD64 and Intel EM64T systems (x64) Multilingual (CC6WDML)
- IBM Db2 Standard Edition - VPC Option - Activation 11.5 for Linux, UNIX and Windows Multilingual (CC36WML ) 
- Jazz for Service Management 1.1.3.0 QuickStart Multiplatform Multilingual (CNC1MML )
- Jazz for Service Management 1.1.3.7 for Linux ML (Launchpad, PRS, Jazz Repository, TDI) Multilingual (CC6QRML )
-  IBM WebSphere Application Server V8.5.5.16 for Jazz for Service Management for Linux Multilingual
- IBM WebSphere Application Server V8.5 Supplements (1 of 3) for Multiplatform Multilingual (CI6X0ML )
-  IBM WebSphere Application Server V8.5 Supplements (2 of 3) for Multiplatform Multilingual (CI6X1ML )
- IBM WebSphere Application Server V8.5 Supplements (3 of 3) for Multiplatform Multilingual (CI6X2ML ) 


#### Get the Omnibis Installables
E-Assembly -> 
- IBM Tivoli Netcool OMNIbus 8.1.0.18 WebGUI - Linux 64bit Multilingual (CC65HML)
- IBM Tivoli Netcool OMNIbus 8.1.0.22 Core - Linux 64bit Multilingual (CC5J4ML)


#### Check Pre-reqs
- unzip then in individual folders.
- Goto PI 1.3.6 Installabled
- Run the prereq_scanner.sh with 'All' option.

#### Step 3: 
Install the required softwares
- gcc
- gcc++
- libstdc++
- Any other missing library
https://www.ibm.com/support/knowledgecenter/en/SSJQQ3_1.3.6/com.ibm.scapi.doc/install_guide/kshandrequiredlibraries.html

- Install JRE `yum install jre`
- Install gcc-c++ `yum install gcc-c++`
- Install perl-XML-Simple `yum install perl-XML-Simple`

#### Step 4: 
Disable SELINUX and restart VM
- vi /etc/selinux/config and specify SELINUX=disabled
- Reboot the VM
