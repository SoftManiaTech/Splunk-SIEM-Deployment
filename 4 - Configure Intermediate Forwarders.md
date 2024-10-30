## Configure Intermediate Forwarders

### Login to Intermediate Forwarder 1

```bash
sudo su splunk
```
```bash
/opt/splunk/bin/splunk status

cd /opt/splunk/bin

./splunk set deploy-poll YOUR_DEPLOYMENT_SERVER_IP:8089

./splunk restart

```
Note: Repeat the above steps for Intermediate Forwarder 2 as well.
