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
