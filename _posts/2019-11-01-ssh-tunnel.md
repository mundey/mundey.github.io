---
published: true
layout: post
title: SSH Tunnel
categories: SSH
tags: devops ssh
author: Jags
---

## SSH Tunnel
SSH Tunnel can be quite useful for a number of tasks when access to required resources are not avaibale from local environment. Few examples are below
- Connect to a DB which allows only connections from a specific source/host
- RDP to a Windows machine in private subnet using bastion host
- Connect DBClient docker such as pgadmin by tunneling through allowed IP

Command Skeleton

ssh -nNT [-i privateKey] {local-ip}:{localport}:{service-host}:{service-port} {user}@{remote-host}
  
Explanation: 
- -nNT are three options used to ensure we are intending to create tunnel and not ssh connection.
-  -i privateKey specify private key if it is not in default (~/.ssh/) location
-  {local-ip} ip address where listening port will start
-  {local-port} this is where connections can be made
-  {service-ip} host or ip address which should be reachable from remote-host
-  {user} username to connect to remote-host
-  {remote-host} where connection is made

Examples:
````shell  
  ssh -nNT -i id_rsa 127.0.0.1:15432:pgdb.example.com:5432 dbuser@bastionhost.example.com
````  
  This command will open a port 15432 on 127.0.0.1 tunneling through pgdb.example.com host which can be accessed only from bastionhost.example.com
