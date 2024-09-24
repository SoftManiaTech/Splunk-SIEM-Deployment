# Increase ulimit values

```bash
cd /etc/security/
```

```bash
vi limits.conf
```
Please check this below link for Splunk recommended ulimit values
https://docs.splunk.com/Documentation/Splunk/9.2.2/Installation/Systemrequirements#Considerations_regarding_system-wide_resource_limits_on_.2Anix_systems

```bash
* soft nofile 64000      # Soft limit for open files (ulimit -n)
* hard nofile unlimited      # Hard limit for open files (ulimit -n)

* soft nproc 16000       # Soft limit for user processes (ulimit -u)
* hard nproc unlimited       # Hard limit for user processes (ulimit -u)

* soft data 8000000      # Soft limit for data segment size (8GB in KB) (ulimit -d)
* hard data unlimited      # Hard limit for data segment size (ulimit -d)

* soft fsize unlimited   # Soft limit for file size (ulimit -f)
* hard fsize unlimited   # Hard limit for file size (ulimit -f)
```
