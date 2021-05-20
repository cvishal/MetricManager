
------
## 3. Install PI Single Server
----
### Install PI (As scadmin user)
- Dir `/home/scadmin/IBM/scanalytics`
- First install DB component only
- Then again go to Installation Manager and click on 'Modify' and add rest of the components.

![Install PI 1 ](/images/pi-install-1.png)
![Install PI 2 ](/images/pi-install-2.png)
![Install PI 3 ](/images/pi-install-3.png)

- Update tablespaces as mentioned here. https://www.ibm.com/support/knowledgecenter/SSJQQ3_1.3.6/com.ibm.scapi.doc/install_guide/t_tsaa_installguide_installingthedb_distributed.html


- Modify to install other components (Keep the database checked)


![Install PI 4 ](/images/pi-install-4.png)
![Install PI 5 ](/images/pi-install-5.png)
![Install PI 6 ](/images/pi-install-6.png)
![Install PI 7 ](/images/pi-install-7.png)
![Install PI 8 ](/images/pi-install-8.png)
![Install PI 9 ](/images/pi-install-9.png)
![Install PI 10](/images/pi-install-10.png)



Post Installation, make sure ncoadmin user has admin rights

In order to allow users access to the Predictive Insights views in DASH, you must run the ‘addAc-cess.sh’ script located under the Predictive Insights UI directory under ‘bin’. For example, if you want to give the ncoadmin admin user access to Predictive Insights, you would run:
`/home/scadmin/IBM/scanalytics/UI/bin/addAccess user ncoadmin admin`

To start the Predictive Insights User Interface, run the following:
`/home/scadmin/IBM/scanalytics/UI/bin/pi.sh -start`



### Verify local PI Installation is working

Login to following 2 URLs with ncoadmin user

https://pi-demo:9998/predictiveinsights/jsp/wlp/wlpAnomalyView.jsp
![Install Complete  ](/images/post-install-1.png)

https://localhost:16311/ibm/console/

Login here as ncoadmin user
Left Navigation -> Event Viewer

![Install Complete  ](/images/post-install-2.png)