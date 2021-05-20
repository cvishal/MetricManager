----
## 2. Install Pre-reqs Softwares for Predictive Insight
-----

### Install DB2
https://www.ibm.com/support/knowledgecenter/en/SSJQQ3_1.3.6/com.ibm.scapi.doc/install_guide/t_tasp_install_installingdb2.html

- Make sure you import license via db2licm uttility


### Switch to user scadmin from here
`su - scadmin`
- Update .bashrc with following:
```
if [ -f /home/db2inst1/sqllib/db2profile ]; then
. /home/db2inst1/sqllib/db2profile
fi
```


### Install Streams
https://www.ibm.com/support/knowledgecenter/en/SSJQQ3_1.3.6/com.ibm.scapi.doc/install_guide/t_tsaa_installguide_infosphere4_install.html

./IBMStreamsSetup.bin

### Install WAS 8.5.5.16 (As scadmin user)

- Get ALL WAS Installables 
- Get IBMIM (IBM Installation Manager)
- https://www.ibm.com/support/pages/installation-manager-and-packaging-utility-download-documents
- Install IBMIM with -aR nonAdmin option 

- Update IBM IM Repo (Was diskTag.inf + Fixpack repository.config) `IBMIM->File->Preferences->Add Repository`
- Install WAS Only (Dont install JDK 7)

- Install WAS on /home/scadmin/IBM/WebSphere/AppServer
- No need to run profiler tool


### Install JazzSM (As scadmin user)
- Install Jazz Service Manager Extention for WAS8.5.5.
![Install JazzSM Extentions](/images/jazzsm-install.png)
- Install DASH 
![Install DASH ](/images/dash-install.png)
![Install DASH ](/images/dash-install-2.png)

- Use vishal as local admin (This avoids conflict if we integrarte with remote LDAP)
- Change TLS Setting as mentioned by https://www.ibm.com/support/knowledgecenter/en/SSJQQ3_1.3.6/com.ibm.scapi.doc/install_guide/t_scapi_installingjazzsm.html

### Install OMNIBus Object Server (As scadmin user)
Need following downloads
- TVL_NTCL_OMN_V8.1.0.22_CORE_LNX_M.zip (Omnibus Object Server)
- TVL_NTCL_OMN_8.1.0.18_WG_LNX.zip (Omnibus WebUI)


Install Omnibus Object Server
- Install Object Server in `/home/scadmin/IBM/tivoli/netcool` folder
- No need to run the Omnibus configuration wizard
- Make sure you follow post install steps https://www.ibm.com/support/knowledgecenter/en/SSJQQ3_1.3.6/com.ibm.scapi.doc/install_guide/t_tasp_install_theomnibusobjectserver.html
- Install missing libraries (libXm, motif, libX11 etc)
- Follow https://www.ibm.com/support/knowledgecenter/en/SSJQQ3_1.3.6/com.ibm.scapi.doc/install_guide/t_tasp_install_configuringtheomnibusobjectserver.html
- Run `nohup ./nco_objserv &` command



### Install OMNIBus WebUI (As scadmin user)
Dir `/home/scadmin/IBM/netcool/gui`
- Configure WEBUI
![Install DASH ](/images/webui-config-1.png)
![Install DASH ](/images/webui-config-2.png)
- Finish configuration

------
