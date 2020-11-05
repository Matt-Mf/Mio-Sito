---
author: "Me"
date: 2020-11-05
title: "Reset commands for Windows network protocol and adapter"
best: false
---
 
Command Prompt (Admin):

*reset windows internet config.
 
```
netsh winsock reset
```
 
*reset TCP/IP 
 
```
netsh int ip reset 
```

*reset ip address

```
ipconfig /release 
```

*refresh ip lease from dhcp
 
```
ipconfig /renew 
```

*flush dns cache
 
```
ipconfig /flushdns 
```

---------------
 
*check the config.
 
```
ipconfig /all
 ```
 
And make sure to check Windows firewall config. as well.
 

 
 
 
 
 
 
 
 
 




