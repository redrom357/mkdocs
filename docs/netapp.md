# NetApp

## Network 

### How to change UTA Port Personality

#### Change adapter mode
```bash
cluster1::> system node hardware unified-connect modify -node cluster1-01 -adapter 1a -mode fc* / cna**
```
*fibre channel
*converged network adapter

#### Reboot the node

### How to telnet from a Netapp to test port availability

#### Unlock diag user and set password
```bash
ONTAP::> security login unlock -username diag

ONTAP::> security login password -username diag
```
#### Go into Privileged Mode
```bash
ONTAP::> set -privilege advanced
```
#### Change to Diag User
```bash
ONTAP::> set diag

ONTAP::> systemshell local
```
#### Once here you can telnet like normal
```bash
ONTAP%>telnet mail.domain.com 25
```
#### To Break out 

CTRL C and CTRL D 

#### Relock Diag Account
```bash
NETAPP::> security login unlock -username diag
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
cDot::*> nfs show -vserver NFSsvm -fields rquotad-port ,nlm-port ,nsm-port ,mountd-port
vserver mountd-port nlm-port nsm-port rquotad-port
------- ----------- -------- -------- ------------
NFSsvm    635         4045     4046     4049

cDot::*>
```

- Alternatively show the ports listening on the node with the following

```bash
cdot::> network connection listening show -node <node name>
Vserver Name     Interface Name:Local Port              Protocol/Service
---------------- -------------------------------------  -----------------------
Node: node 1
Cluster          node1_clus1:7700                       TCP/ctlopcp
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
affa220-1-cluster::> event log show -node <node> -seqnum <seqnum>

                  Node: <node>
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
cluster::> vscan connection-status show -node <node> -vserver <vserver>
  (vserver vscan connection-status show)

                           Node: <node>
                        Vserver: <vserver>
List of Connected Vscan Servers: <vscan_server>
Number of Connected Vscan Servers Serving the Vserver: 1
```

## Cluster peer 

### How to check cluster peer health 

#### Check peer health

```bash
cluster::> cluster peer health show
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
cluster::> cluster peer ping
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