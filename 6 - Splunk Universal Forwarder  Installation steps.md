## Step-1 : Become root user
Login as "root" user using below command
```bash
sudo su 
```
## Step-2 : Create new user (splunk), directories & permissions

Create user & group

```bash
sudo adduser splunk
```
Create directory
```bash
mkdir /opt/splunkforwarder
```

Change the ownership of the created directory to the new user **"splunk"** (hereafter will be called as splunk user)

```bash
chown -R splunk:splunk /opt/splunkforwarder/
```


Verify the ownership of the directory
```bash
ll /opt/
```

Install **"wget"**
```bash
yum install wget
```

## Step-3 : Splunk Universal Forwarder Installation

Switch to splunk user 
```bash
sudo su - splunk
```

Navigate to splunk user home directory
```bash
cd /home/splunk
```

Download Splunk Universal Forwarder (Based on the version you want, you can get this command from (https://www.splunk.com/en_us/download/universal-forwarder.html?locale=en_us))
```bash
wget -O splunkforwarder-9.2.2-d76edf6f0a15-Linux-x86_64.tgz "https://download.splunk.com/products/universalforwarder/releases/9.2.2/linux/splunkforwarder-9.2.2-d76edf6f0a15-Linux-x86_64.tgz"
```

Extract the tar package
```bash
tar -xvf splunkforwarder-9.2.2-d76edf6f0a15-Linux-x86_64.tgz -C /opt/
```

Navigate to Splunk bin directory
```bash
cd /opt/splunkforwarder/bin
```

Start the Splunk with accepting license & setting the default username (admin) passing the passowrd (Pa55word)
```bash
./splunk start --accept-license --no-prompt --answer-yes --seed-passwd YOUR_PASSWORD
```

**Note:** In above step installer will ask you to create username and password, please keep these credentials safe (These are the admin credentials which you will use to Manage Splunk)

At this point, universal Forwarder is installed in your linux server

## Step-4: Configure Splunk to run at boot time

Exit from splunk user & sign in as **root** user
``` bash
exit
sudo su 
```

Stop the Forwarder, Enable boot start and start the Forwarder again
``` bash
/opt/splunkforwarder/bin/splunk stop
/opt/splunkforwarder/bin/splunk enable boot-start -user splunk
/opt/splunkforwarder/bin/splunk start
```
That's it... you have successfully installed Splunk Universal forwarder on Linux..!!

## Connect universal forwarder to Deployment server

```bash
sudo su splunk

cd /opt/splunkforwarder/bin

./splunk set deploy-poll YOUR_DEPLOYMENT_SERVER_IP:8089

```
Exit from splunk user & sign in as **root** user
``` bash
exit
sudo su 
```
Restart the Universal Forwarder
```bash
/opt/splunkforwarder/bin/splunk restart
```



