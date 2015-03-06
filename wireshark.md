Wireshark Filter CheatSheet
---------------------------

Here are some example filters for wireshark.

## GET requests from a specific client (192.168.0.120)

```
 ip.src == 192.168.0.120 and http.request.method == "GET"
```

## TCP traffic on port 23 to and from 192.168.0.1

```
tcp port 23 and host 192.168.0.1
```
