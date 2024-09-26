```bash
sudo su
```

```bash
yum update -y
useradd splunk
groupadd splunk
mkdir /opt/splunk
ll /opt/
chown -R splunk:splunk /opt/splunk/
ll /opt/
yum install wget -y
```

```bash
sudo su - splunk
```

```bash
cd /home/splunk
wget -O splunk-9.2.2-d76edf6f0a15-Linux-x86_64.tgz "https://download.splunk.com/products/splunk/releases/9.2.2/linux/splunk-9.2.2-d76edf6f0a15-Linux-x86_64.tgz"
tar -xvf splunk-9.2.2-d76edf6f0a15-Linux-x86_64.tgz -C /opt/
cd /opt/splunk/bin
./splunk start --accept-license --no-prompt --answer-yes --seed-passwd admin123
exit
```

```bash
sudo su
```

```bash
/opt/splunk/bin/splunk stop
```

```bash
/opt/splunk/bin/splunk enable boot-start -user splunk
```

```bash
/opt/splunk/bin/splunk start
```
