## Connect Search Head Cluster with Indexer Cluster

### Search Head 1, 2, 3
```bash
sudo su - splunk
```
```bash
cd /opt/splunk/bin

./splunk edit cluster-config -mode searchhead -manager_uri https://YOUR_CLUSTER_MANAGER_IP:8089 -secret YOUR_INDEXER_CLUSTER_SECRET_KEY 

./splunk restart
```

## Connect Forwarders with Indexer Cluster

### Best Practice: Implement Indexer Discovery

#### In Cluster Manager

```bash
sudo su - splunk
```
```bash
cd /opt/splunk/etc/system/local/

vi server.conf

[indexer_discovery]
pass4SymmKey = YOUR_INDEXER_DISCOVERY_KEY
polling_rate = 10
indexerWeightByDiskCapacity = true

/opt/splunk/bin/splunk restart

```

#### In Deployment Server

```bash
sudo su - splunk
```
```bash
cd /opt/splunk/etc/deployment-apps

mkdir ORG_general_infra_config

cd ORG_general_infra_config

mkdir local

cd local

ls

vi outputs.conf

[indexer_discovery:manager1]
pass4SymmKey = YOUR_INDEXER_DISCOVERY_KEY
manager_uri = https://your_cluster_manager_ip:8089

[tcpout:group1]
autoLBFrequency = 30
forceTimebasedAutoLB = true
indexerDiscovery = manager1
useACK=true

[tcpout]
defaultGroup = group1

```

### In Deployer 

```bash
sudo su - splunk
```
```bash

cd /opt/splunk/etc/shcluster/apps/ 

mkdir ORG_general_infra_config

cd ORG_general_infra_config

mkdir local

cd local

ls

vi outputs.conf

[indexer_discovery:manager1]
pass4SymmKey = YOUR_INDEXER_DISCOVERY_KEY
manager_uri = https://your_cluster_manager_ip:8089

[tcpout:group1]
autoLBFrequency = 30
forceTimebasedAutoLB = true
indexerDiscovery = manager1
useACK=true

[tcpout]
defaultGroup = group1

cd /opt/splunk/bin/

./splunk show shcluster-status --verbose

./splunk apply shcluster-bundle --answer-yes -target https://SEARCH_HEAD_1_IP:8089 -auth admin:PASSWORD

```


### In Cluster Manager 

```bash
sudo su - splunk
```
```bash
cd /opt/splunk/etc/apps/ 

mkdir ORG_general_infra_config

cd ORG_general_infra_config

mkdir local

cd local

ls

vi outputs.conf

[indexer_discovery:manager1]
pass4SymmKey = YOUR_INDEXER_DISCOVERY_KEY
manager_uri = https://your_cluster_manager_ip:8089

[tcpout:group1]
autoLBFrequency = 30
forceTimebasedAutoLB = true
indexerDiscovery = manager1
useACK=true

[tcpout]
defaultGroup = group1

cd /opt/splunk/bin/

./splunk restart

```

