
## Configure Indexer Cluster 

### Cluster Manager:

#### Login to Cluster Manager using SSH:
```bash
sudo su - splunk
```

```bash
cd /opt/splunk/bin

./splunk edit cluster-config -mode manager -replication_factor 3 -search_factor 2 -secret YOUR_KEY -cluster_label cluster1

./splunk restart
```

### Peer nodes (All indexers)

#### Login to peer node using SSH:
```bash
sudo su - splunk
```
```bash
cd /opt/splunk/bin

./splunk edit cluster-config -mode peer -manager_uri https://YOUR_CLUSTER_MANAGER_IP:8089 -replication_port 9887 -secret YOUR_KEY

./splunk restart
```
