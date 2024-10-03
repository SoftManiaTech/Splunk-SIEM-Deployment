## Configure Search Head Cluster

### Enable Deployer

#### Login to Deployer using SSH

##### Navigate to system/local directory.
```bash
sudo su splunk
```
```bash
cd /opt/splunk/etc/system/local/
```

#### Add below contents to server.conf file.
```bash
vi server.conf
```
```bash
[shclustering]
pass4SymmKey = SoftManiaSHClusterKey
shcluster_label = shcluster1
```
#### Restart the Deployer.

```bash
/opt/splunk/bin/splunk restart
```

## Configure Search Head cluster members

### Search Head 1

#### Execute below commands
```bash
sudo su splunk

cd /opt/splunk/bin

./splunk init shcluster-config -auth admin:YOUR_PASSWD -mgmt_uri https://YOUR_SH1_IP:8089 -replication_port 9000 -replication_factor 3 -conf_deploy_fetch_url http://YOUR_DEPLOYER_IP:8089 -secret pass_4_Symm_Key -shcluster_label shcluster1

./splunk restart
```
### Search Head 2

#### Execute below commands
```bash
sudo su splunk

cd /opt/splunk/bin

./splunk init shcluster-config -auth admin:YOUR_PASSWD -mgmt_uri https://YOUR_SH2_IP:8089 -replication_port 9000 -replication_factor 3 -conf_deploy_fetch_url http://YOUR_DEPLOYER_IP:8089 -secret pass_4_Symm_Key -shcluster_label shcluster1

./splunk restart
```
### Search Head 3

#### Execute below commands
```bash
sudo su splunk

cd /opt/splunk/bin

./splunk init shcluster-config -auth admin:YOUR_PASSWD -mgmt_uri https://YOUR_SH3_IP:8089 -replication_port 9000 -replication_factor 3 -conf_deploy_fetch_url http://YOUR_DEPLOYER_IP:8089 -secret pass_4_Symm_Key -shcluster_label shcluster1

./splunk restart
```

## Bootstrap Search Head cluster election
In Search Head 1,

```bash
sudo su splunk

cd /opt/splunk/bin

./splunk bootstrap shcluster-captain -servers_list "https://YOUR_SH1_IP:8089,https://YOUR_SH2_IP:8089,https://YOUR_SH3_IP:8089" -auth admin:YOUR_SH1_PASSWORD

./splunk show shcluster-status -auth admin:YOUR_SH1_PASSWORD
```
