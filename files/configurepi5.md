
------

## 10. ReConfigure PI Analytics UI to connect to remote LDAP
-----


#### Follow these 3 steps:
https://www.ibm.com/support/knowledgecenter/SSJQQ3_1.3.6/com.ibm.scapi.doc/admin_guide/t_oapi_adminguide_configureUIldap.html


#### Step 1: Configure the LDAP user registry.
- cd /home/scadmin/IBM/scanalytics/UI/wlp/usr/servers/piserver 
- Create new ldapRegistry.xml file. Here is my working copy of the same file

```
<server>
<ldapRegistry id="ldap" realm="defaultWIMFileBasedRealm" baseDN="dc=mycluster,dc=icp" host="169.46.14.148" port="31230" ignoreCase="true"
bindDN="cn=admin,dc=mycluster,dc=icp" bindPassword="NSc3hd1Hq6oPvyR"
ldapType="Custom" sslEnabled="false" >

<idsFilters userFilter="(&amp;(uid=%v)(objectclass=ePerson))"
groupFilter="(&amp;(cn=%v)(|(objectclass=groupOfNames)(objectclass=groupOfUniqueNames)
objectclass=groupOfURLs)))" userIdMap="*:uid"
groupIdMap="*:cn"
groupMemberIdMap="mycompany-allGroups:member;mycompany-allGroups:uniqueMember;
groupOfNames:member;groupOfUniqueNames:uniqueMember">
</idsFilters>
</ldapRegistry>
</server>
```

- Update server.xml with the necessary changes mentioned in above KC link
- restart piserver

#### Step 2: Give required Access 
- cd /home/scadmin/IBM/scanalytics/UI/bin
- ./addAccess.sh group PI_admins admin
- ./addAccess.sh user ncoadmin admin
- ./addAccess.sh user icpadmin admin


#### Step 3: Validate

Follow Steps https://www.ibm.com/support/knowledgecenter/SSJQQ3_1.3.6/com.ibm.scapi.doc/admin_guide/t_oapi_adminguide_verifyldap.html

