Sample data - /var/log/messages

```bash
2024-09-11 10:00:00 ERROR An error occurred in the application
2024-09-11 10:01:00 INFO Application started successfully
2024-09-11 10:02:00 DEBUG Debugging connection issues
2024-09-11 10:03:00 ERROR Failed to load configuration file
2024-09-11 10:04:00 INFO User logged in successfully
```

Let's say All ERROR data should go to error_idx, INFO data should go to info_idx, DEBUG data should go to debug_idx

In Universal Forwarder

Assume we have below inputs.conf stanza

```bash
[monitor:///var/log/messages]
disabled = false
index = default   # This will be overridden by transforms.conf
```

In Intermediate Forwarder, add below contents (If you have deployment server, go to the respective app that coontains the configurations for Intermediate Forwarders)

props.conf
```bash
[source::/var/log*]
TRANSFORMS-setindex = route_to_index1, route_to_index2, route_to_index3
```

transforms.conf
```bash
[route_to_index1]
REGEX = WARN
DEST_KEY = _MetaData:Index
FORMAT = warn_idx

[route_to_index2]
REGEX = INFO
DEST_KEY = _MetaData:Index
FORMAT = info_idx

[route_to_index3]
REGEX = DEBUG
DEST_KEY = _MetaData:Index
FORMAT = debug_idx
```
