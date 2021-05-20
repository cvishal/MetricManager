------
## 4. Get Required Details of Event Manager on OCP
----

For this we need to collect following details for target OCP based Watson AIOps Event Manager

URL to login :
`https://netcool.noi.gsi-waiops-4c84f19c22c6eb1784ba9d2966faea77-0000.us-south.containers.appdomain.cloud`
UID: `smadmin`
PW: `xxxxxx`

### Get all details for Object Server
IP : Get IP address for above URL which would be Load Balancer IP address

```
vishal@~>nslookup netcool.noi.gsi-waiops-4c84f19c22c6eb1784ba9d2966faea77-0000.us-south.containers.appdomain.cloud
Server:		49.205.72.130
Address:	49.205.72.130#53

Non-authoritative answer:
netcool.noi.gsi-waiops-4c84f19c22c6eb1784ba9d2966faea77-0000.us-south.containers.appdomain.cloud	canonical name = gsi-waiops-4c84f19c22c6eb1784ba9d2966faea77-0000.us-south.containers.appdomain.cloud.
Name:	gsi-waiops-4c84f19c22c6eb1784ba9d2966faea77-0000.us-south.containers.appdomain.cloud
Address: 169.46.14.148

vishal@~>

```
`Hostname would be LB IP Address which is 169.46.14.148 in my case`

```
- Object Server host details = 169.46.14.xxx (As Mentioned Above Step)
- UID for Object Server = root (Standard User for Object Server)
- PW for Object Server =  (Need to retrieve. Instructions Below)
- NodePort for Object Server = (Need to retrieve. Instructions Below)
```

### Need to expose LDAP port

Run command
- `oc get pods | grep -i ldap`
- get 'noi-openldap-0' pod name
- `oc expose po noi-openldap-0 --port=389 --type=NodePort --name=ldapsvc-nodeport`
- get port number
- `oc get svc | grep -i ldap`
- Read and record Node Port

### Make sure you disable Network Policy on OCP-NOI so it allows ingress traffic

```
- oc get NetworkPolicy
- Look for noi-ibm-netcool-prod-network-policy
- oc describe NetworkPolicy noi-ibm-netcool-prod-network-policy (You will find its retricted)
- Edit the policy to have following:

spec:
  ingress:
  - {}
  podSelector: {}
  policyTypes:
  - Ingress

```
### Verify details
```
LDAP Server Host details = 169.46.14.148 (on my setup)
LDAP Server Node Port = 31230 (on my setup)
```

Telnet to validate it works.


### Get the LDAP Bind DN and password OCP nachine

```
[root@vishnfs1 ~]# oc get secret | grep -i ldap
noi-ldap-secret                                                   Opaque                                1      35d
[root@vishnfs1 ~]# 
[root@vishnfs1 ~]# oc get secret noi-ldap-secret -o yaml
apiVersion: v1
data:
  LDAP_BIND_PASSWORD: xxxxxxxxxxxxxx
kind: Secret
metadata:
  creationTimestamp: "2021-02-15T12:04:16Z"
  managedFields:
  - apiVersion: v1
    fieldsType: FieldsV1
    fieldsV1:
      f:data:
        .: {}
        f:LDAP_BIND_PASSWORD: {}
      f:type: {}
    manager: curl
    operation: Update
    time: "2021-02-15T12:04:16Z"
  name: noi-ldap-secret
  namespace: dev-aiops
  resourceVersion: "62332819"
  selfLink: /api/v1/namespaces/dev-aiops/secrets/noi-ldap-secret
  uid: 6b653619-10fe-49b3-9ce5-1a259fb0e645
type: Opaque
[root@vishnfs1 ~]# 
[root@vishnfs1 ~]# echo TlNjM2hkMUhxNm9QdnlS | base64 -d
NSc3hd1Hq6oPvyR
[root@vishnfs1 ~]# 
```

Bind DN => Copy from EM WAS Consile
Bind Password => xxxxxxxxxx


### Get the WAS smadmin password on OCP nachine

```
[root@vishnfs1 ~]# oc get secret noi-was-secret -o yaml
apiVersion: v1
data:
  WAS_PASSWORD: xxxxxxxxxx
kind: Secret
metadata:
  creationTimestamp: "2021-02-15T12:04:16Z"
  managedFields:
  - apiVersion: v1
    fieldsType: FieldsV1
    fieldsV1:
      f:data:
        .: {}
        f:WAS_PASSWORD: {}
      f:type: {}
    manager: curl
    operation: Update
    time: "2021-02-15T12:04:16Z"
  name: noi-was-secret
  namespace: dev-aiops
  resourceVersion: "62332821"
  selfLink: /api/v1/namespaces/dev-aiops/secrets/noi-was-secret
  uid: a3e611dd-8c21-4053-ab1f-5ae0888ab9e2
type: Opaque
[root@vishnfs1 ~]# echo xxxxxxxxx | base64 -d
yyyyyyy
[root@vishnfs1 ~]#
```
