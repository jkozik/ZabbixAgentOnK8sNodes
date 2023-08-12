# Zabbix Agent on Kubernetes Node
It is really simple to add a basic zabbix agent to each kubernetes nodes in your cluster.  I run the agent in a container in active mode. I manually name and configure each nodes as a zabbix host ((Template OS Linux by Zabbix agent active) -- no autoregistration.
I created a group called K8s Nodes. 
Here's an example of how I setup my node called kmaster.
## Install zabbix agent on k8s node
```
[jkozik@kmaster ~]$ docker run --name zabbix-agent -e ZBX_ACTIVESERVERS="linode3.kozik.net" \
>    -e ZBX_HOSTNAME="kmaster" \
>    -d zabbix/zabbix-agent:alpine-6.0-latest
520f20ee943389ff82f587a5f532d6556edac516d0bc5909d8287ab76d64e687
[jkozik@kmaster ~]$ docker logs zabbix-agent
** Preparing Zabbix agent
** Preparing Zabbix agent configuration file
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "PidFile": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "LogType": 'console'...added
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "LogFile": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "LogFileSize": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "DebugLevel": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "SourceIP": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "LogRemoteCommands": ''...removed
** Using 'zabbix-server' servers for passive checks
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "Server": 'zabbix-server'...updated
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "ListenPort": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "ListenIP": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "ListenBacklog": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "StartAgents": ''...removed
** Using 'zabbix-server:10051,linode3.kozik.net' servers for active checks
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "ServerActive": 'zabbix-server:10051,linode3.kozik.net'...updated
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "HostInterface": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "HostInterfaceItem": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "Hostname": 'kmaster'...updated
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "HostnameItem": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "HostMetadata": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "HostMetadataItem": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "RefreshActiveChecks": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "BufferSend": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "BufferSize": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "MaxLinesPerSecond": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "Timeout": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "Include": '/etc/zabbix/zabbix_agentd.d/*.conf'...added first occurrence
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "UnsafeUserParameters": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "LoadModulePath": '/var/lib/zabbix/modules/'...added
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSConnect": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSAccept": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSCAFile": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSCRLFile": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSServerCertIssuer": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSServerCertSubject": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSCertFile": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSCipherAll": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSCipherAll13": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSCipherCert": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSCipherCert13": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSCipherPSK": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSCipherPSK13": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSKeyFile": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSPSKIdentity": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "TLSPSKFile": ''...removed
** Updating '/etc/zabbix/zabbix_agentd.conf' parameter "User": 'zabbix'...added
Starting Zabbix Agent [kmaster]. Zabbix 6.0.19 (revision 998f864).
Press Ctrl+C to exit.

     8:20230812:191734.257 Starting Zabbix Agent [kmaster]. Zabbix 6.0.19 (revision 998f864).
     8:20230812:191734.257 **** Enabled features ****
     8:20230812:191734.257 IPv6 support:          YES
     8:20230812:191734.257 TLS support:           YES
     8:20230812:191734.257 **************************
     8:20230812:191734.257 using configuration file: /etc/zabbix/zabbix_agentd.conf
     8:20230812:191734.258 agent #0 started [main process]
    83:20230812:191734.258 agent #1 started [collector]
    84:20230812:191734.259 agent #2 started [listener #1]
    85:20230812:191734.261 agent #3 started [listener #2]
    86:20230812:191734.264 agent #4 started [listener #3]
    87:20230812:191734.267 agent #5 started [active checks #1]
    88:20230812:191734.271 agent #6 started [active checks #2]
    87:20230812:191734.310 Unable to connect to [zabbix-server]:10051 [cannot resolve [zabbix-server]]
    87:20230812:191734.310 Active check configuration update started to fail
```
