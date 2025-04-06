# NetApp

## Network 

### VLAN Configuration

#### Create a VLAN interface

```bash
cluster1::> network port vlan create -node cluster1-01 -vlan-name a0a-15
cluster1::> network port vlan create -node cluster1-02 -vlan-name a0a-15
```

#### Add VLAN interface to a broadcast domain

```bash
cluster1::> network port broadcast-domain add-ports -ipspace Default -broadcast-domain DeptB -ports cluster1-01:a0a-15
cluster1::> network port broadcast-domain add-ports -ipspace Default -broadcast-domain DeptB -ports cluster1-02:a0a-15
cluster1::> network port vlan show
```

### Subnet Configuration

#### Create a Subnet

```bash
cluster1::> network subnet create -ipspace Default -subnet-name DeptB -broadcast-domain DeptB -subnet 172.23.15.2/255.255.255.0 -gateway 172.23.15.254 -ip-ranges 172.23.15.21-172.23.15.40 -force-upudate-lif-association
cluster1::> network subnet show
```

### Create a Data LIF

#### Create a Data LIF using a Subnet

```bash
cluster1::> network interface create -vserver DeptB -lif cluster1-01_cifs -role data -data-protocol cifs -subnet-name DeptB -home-node cluster1-01 -home-port a0a-15
cluster1::> network interface create -vserver DeptB -lif cluster1-02_cifs -role data -data-protocol cifs -subnet-name DeptB -home-node cluster1-02 -home-port a0a-15
cluster1::> network interface create -vserver DeptB -lif cluster1-01_nfs -role data -data-protocol nfs -subnet-name DeptB -home-node cluster1-01 -home-port a0a-15
cluster1::> network interface create -vserver DeptB -lif cluster1-02_nfs -role data -data-protocol nfs -subnet-name DeptB -home-node cluster1-02 -home-port a0a-15
cluster1::> network interface create -vserver DeptB -lif cluster1-01_iscsi -role data -data-protocol iscsi -subnet-name DeptB -home-node cluster1-01 -home-port a0a-15
cluster1::> network interface create -vserver DeptB -lif cluster1-02_iscsi -role data -data-protocol iscsi -subnet-name DeptB -home-node cluster1-02 -home-port a0a-15
cluster1::> network interface show
cluster1::> network interface show -vserver DeptB -lif cluster1-01_cifs
```

### How to change UTA Port Personality

#### Change adapter mode
```bash
cluster1-01::> system node hardware unified-connect modify -node cluster1-01 -adapter 1a -mode fc* / cna**
```
*fibre channel
*converged network adapter

#### Reboot the node

### How to telnet from a Netapp to test port availability

#### Unlock diag user and set password
```bash
cluster1::> security login unlock -username diag

cluster1::> security login password -username diag
```
#### Go into Privileged Mode
```bash
cluster1::> set -privilege advanced
```
#### Change to Diag User
```bash
cluster1::> set diag

cluster1::> systemshell local
```
#### Once here you can telnet like normal
```bash
cluster1%>telnet mail.domain.com 25
```
#### To Break out 

CTRL C and CTRL D 

#### Relock Diag Account
```bash
cluster1::> security login unlock -username diag
```

### Which Network File System (NFS) TCP and NFS UDP ports are used on the storage system?

- The default ports used by the storage controller are as follows:

```
111   TCP/UDP portmapper
2049  TCP/UDP nfsd
635   TCP/UDP mountd
4045  TCP/UDP nlockmgr
4046  TCP/UDP status
4049  TCP/UDP rquotad
```

- It is possible to modify those default ports, therefore to check the currently configured ports on your storage controller please use the following commands,

```bash
cluster1::*> nfs show -vserver NFSsvm -fields rquotad-port ,nlm-port ,nsm-port ,mountd-port
vserver mountd-port nlm-port nsm-port rquotad-port
------- ----------- -------- -------- ------------
NFSsvm    635         4045     4046     4049

cluster1::*>
```

- Alternatively show the ports listening on the node with the following

```bash
cluster1::> network connection listening show -node <node name>
Vserver Name     Interface Name:Local Port              Protocol/Service
---------------- -------------------------------------  -----------------------
Node: cluster1-01
Cluster          cluster1-01:7700                       TCP/ctlopcp
vs01             VS01_lif01:40001                       TCP/cifs-msrpc
VS01             VS01_lif01:135                         TCP/cifs-msrpc
VS01             VS01_lif01:4049                        UDP/unknown
```

- These ports list can also be seen from from most unix clients with the command: rpcinfo -p <storage-controller-IP>

```bash
 program vers proto   port  service
    100000    2   udp    111  portmapper
    100000    2   tcp    111  portmapper
    100000    3   udp    111  portmapper
    100000    3   tcp    111  portmapper
    100000    4   udp    111  portmapper
    100000    4   tcp    111  portmapper
    100003    3   udp   2049  nfs
    100003    3   tcp   2049  nfs
    100003    4   tcp   2049  nfs
    100005    1   udp    635  mountd
    100005    2   udp    635  mountd
    100005    3   udp    635  mountd
    100005    1   tcp    635  mountd
    100005    2   tcp    635  mountd
    100005    3   tcp    635  mountd
    100021    4   udp   4045  nlockmgr
    100021    4   tcp   4045  nlockmgr
    100024    1   udp   4046  status
    100024    1   tcp   4046  status
```

## Antivirus

### How to check vscan server status

#### You received the following alert
```bash
cluster1::> event log show -node cluster1-01 -seqnum <seqnum>

                  Node: cluster1-01
             Sequence#: 5290401
                  Time: 3/3/2025 12:51:24
              Severity: EMERGENCY
                Source: nblade2
          Message Name: Nblade.vscanNoScannerConn
                 Event: Nblade.vscanNoScannerConn: Vserver "<svm>" has no virus scanner connection.
     Corrective Action: Ensure that the scanner pool is properly configured and the AV servers are active and connected to ONTAP.
           Description: This message occurs when ONTAP(R) has no vscan connection for servicing virus scan-requests. This might cause data unavailability if the scan-mandatory option is enabled.
```

#### Check the connection status on the affected node and vserver

```bash
cluster1::> vscan connection-status show -node cluster1-01 -vserver <vserver>
  (vserver vscan connection-status show)

                           Node: cluster1-01
                        Vserver: <vserver>
List of Connected Vscan Servers: <vscan_server>
Number of Connected Vscan Servers Serving the Vserver: 1
```

## Cluster peer 

### How to check cluster peer health 

#### Check peer health

```bash
cluster1::> cluster peer health show
Node       Cluster-Name                 Node-Name
             Ping-Status               RDB-Health Cluster-Health Availability
---------- --------------------------- --------- --------------- ------------
nodea dest-cluster      dest-nodea
             Data: interface_reachable
             ICMP: -                   true      true            true
                                       dest-nodeb
             Data: interface_reachable
             ICMP: -                   true      true            true
nodeb dest-cluster      dest-nodea
             Data: interface_reachable
             ICMP: -                   true      true            true
                                       dest-nodeb
             Data: interface_reachable
             ICMP: -                   true      true            true
4 entries were displayed.
```

#### Ping peer nodes

```bash
cluster1::> cluster peer ping
Node: nodea        Destination Cluster: cluster
Destination Node IP Address       Count  TTL RTT(ms) Status
---------------- ---------------- ----- ---- ------- -------------------------
nodea  10.59.25.243         1   64 0.08500000000000001 interface_reachable
nodea  10.59.25.244         1   64   0.098 interface_reachable
nodeb  10.59.25.245         1   64   0.341 interface_reachable
nodeb  10.59.25.246         1   64   0.334 interface_reachable
Node: nodea        Destination Cluster: dest-cluster
Destination Node IP Address       Count  TTL RTT(ms) Status
---------------- ---------------- ----- ---- ------- -------------------------
dest-nodea  10.59.25.247         1   64   0.838 interface_reachable
dest-nodea  10.59.25.248         1   64   1.403 interface_reachable
dest-nodeb  10.59.25.249         1   64   0.639 interface_reachable
dest-nodeb  10.59.25.250         1   64   1.395 interface_reachable
Node: nodeb        Destination Cluster: cluster
Destination Node IP Address       Count  TTL RTT(ms) Status
---------------- ---------------- ----- ---- ------- -------------------------
nodea  10.59.25.243         1   64   0.174 interface_reachable
nodea  10.59.25.244         1   64   0.481 interface_reachable
nodeb  10.59.25.245         1   64   0.157 interface_reachable
nodeb  10.59.25.246         1   64   0.066 interface_reachable
Node: nodeb        Destination Cluster: dest-cluster
Destination Node IP Address       Count  TTL RTT(ms) Status
---------------- ---------------- ----- ---- ------- -------------------------
dest-nodea  10.59.25.247         1   64   0.796 interface_reachable
dest-nodea  10.59.25.248         1   64   1.434 interface_reachable
dest-nodeb  10.59.25.249         1   64   0.756 interface_reachable
dest-nodeb  10.59.25.250         1   64   1.525 interface_reachable
16 entries were displayed.
```

https://kb.netapp.com/on-prem/ontap/Ontap_OS/OS-KBs/Why_does_cpeer_unavailable_alert_occur_even_peering_status_is_interface_reachable

## Privileged modes

### Set privileged advanced mode in nodeshell

```bash
cluster1::*> system node run -node cluster1-01
Type 'exit' or 'Ctrl-D' to return to the CLI
cluster1-01> priv set advanced
Warning: These advanced commands are potentially dangerous; use
         them only when directed to do so by NetApp
         personnel.
cluster1-01*> ls /etc
.
[...]
```

### Unlock, set password and login to diag account

#### Unlock diag account 

```bash
cluster1::*> security login show -username diag

Vserver: cluster1
                                                                 Second
User/Group                 Authentication                 Acct   Authentication
Name           Application Method        Role Name        Locked Method
-------------- ----------- ------------- ---------------- ------ --------------
diag           console     password      admin            yes    none

cluster1::*> security login unlock -username diag

cluster1::*> security login show -username diag

Vserver: cluster1
                                                                 Second
User/Group                 Authentication                 Acct   Authentication
Name           Application Method        Role Name        Locked Method
-------------- ----------- ------------- ---------------- ------ --------------
diag           console     password      admin            no     none
```

#### Set password diag account 

```bash
cluster1::*> security login password -username diag

Enter a new password: ******
Enter it again: ******
```

#### Login to diag account

```bash
cluster1::*> systemshell -node cluster1-01
  (system node systemshell)
diag@127.0.0.1's password:

Warning:  The system shell provides access to low-level
diagnostic tools that can cause irreparable damage to
the system if not used properly.  Use this environment
only when directed to do so by support personnel.

cluster1-01%
```


