# NetApp

## How to telnet from a Netapp to test port availability

### Unlock diag user and set password
```bash
ONTAP::> security login unlock -username diag

ONTAP::> security login password -username diag
```
### Go into Privileged Mode
```bash
ONTAP::> set -privilege advanced
```
### Change to Diag User
```bash
ONTAP::> set diag

ONTAP::> systemshell local
```
### Once here you can telnet like normal
```bash
ONTAP%>telnet mail.domain.com 25
```
### To Break out 

CTRL C and CTRL D 

### Relock Diag Account
```bash
NETAPP::> security login unlock -username diag
```

## Which Network File System (NFS) TCP and NFS UDP ports are used on the storage system?

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
