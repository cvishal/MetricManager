
------
## 7. Update Local DASH to point to remote Object Server
------

### Make sure PI-DASH points to remote object server (OCP Based EM Object Server) to retrieve events.

#### Retrieve NodePort of Object Server Primary and Backup

- Use Following command:
```
[root@vishnfs1 ~]# oc get svc | grep -i noi-objserv-agg-
noi-objserv-agg-backup                                           ClusterIP   172.21.95.89     <none>        4100/TCP,4300/TCP                                       38d
noi-objserv-agg-backup-nodeport                                  NodePort    172.21.141.70    <none>        4100:31198/TCP,32428:32428/TCP                          38d
noi-objserv-agg-primary                                          ClusterIP   172.21.167.194   <none>        4100/TCP                                                38d
noi-objserv-agg-primary-nodeport                                 NodePort    172.21.13.199    <none>        4100:31483/TCP,32525:32525/TCP                          38d

```
- Primary Object Server NodePort = 31483
- Backup Object Server NodePort = 31198
- Hostname would be same as LB HostName = 169.46.14.xxx 

#### Update the Data Source Definition File for omnibus webui

```
cd /home/scadmin/IBM/netcool/gui/omnibus_webgui/etc/datasources
cp ncwDataSourceDefinitions.xml ncwDataSourceDefinitions.xml_bkp
vi ncwDataSourceDefinitions.xml
```

- Update 1 (Add root and password correctly)

```
 <ncwDataSourceCredentials
            userName="root" password="xxxxxxxxxxxx"
            encrypted="false"
        />
```
- Update 2 (Add remote Object Server Details. Check ncwOSConnection)        
```
 <ncwFailOverPairDefinition>
            <!--
             ! The primary ObjectServer to connect to.
             ! - host : The hostname or IP address of the server the ObjectServer is installed on.
             ! - port : The port number the ObjectServer is listening on.
             ! - ssl  : Enables SSL connection to the ObjectServer. [false|true]
             ! - minPoolSize : Specifies the minimum number of connections that will be added to the connection pool. Default value is 5.
             ! - maxPoolSize : Specifies the maximum number of connections that will be added to the connection pool. Default value is 10.
             !-->
            <ncwPrimaryServer>
                <ncwOSConnection host="169.46.14.148" port="31483" ssl="false" minPoolSize="5" maxPoolSize="10"/>
            </ncwPrimaryServer>

            <!--
             ! The optional failover ObjectServer to connect to.
             !-->
            <!--
            <ncwBackUpServer>
                <ncwOSConnection host="169.46.14.xxx" port="31198" ssl="false" minPoolSize="5" maxPoolSize="10"/>
            </ncwBackUpServer>
            -->
        </ncwFailOverPairDefinition>

    </ncwDataSourceDefinition>
```

#### Restart omnibus webui using following commands
 
Restart JazzSM Instance (omnibus webui)
- `cd /home/scadmin/IBM/JazzSM/profile/bin/stopServer.sh server1`
- Use vishal and password to stop server
- `cd /home/scadmin/IBM/JazzSM/profile/bin/startServer.sh server1`

