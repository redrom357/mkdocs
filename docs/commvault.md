# Commvault

## HyperscaleX

### Check Hedvig services

### With hsx_collect script

```bash
./hsx_collectsh -services
[root@<hostname>11 ~]# /hsx_collectsh -services
Report service status
Cluster Name: HV12345678912345
Cluster Nodes:
<hostname>11   - Last reboot - 2025-03-12 08:01:46
<hostname>12   - Last reboot - 2025-03-10 09:28:12
<hostname>13   - Last reboot - 2025-02-23 18:11:41
<hostname>14   - Last reboot - 2025-02-24 22:24:40
<hostname>15   - Last reboot - 2025-02-24 23:58:32
<hostname>16   - Last reboot - 2025-02-25 01:30:14
* - Deploy node

CDS Service Status Check:
hedvighblock
|_  <hostname>11 hedvighblock    Active: active (running) since Wed 2025-03-12 09:05:33 CET; 1h 34min ago
|_  <hostname>12 hedvighblock    Active: active (running) since Wed 2025-03-12 09:17:24 CET; 1h 22min ago
|_  <hostname>13 hedvighblock    Active: active (running) since Tue 2025-02-25 12:48:08 CET; 2 weeks 0 days ago
|_  <hostname>14 hedvighblock    Active: active (running) since Tue 2025-02-25 12:48:08 CET; 2 weeks 0 days ago
|_  <hostname>15 hedvighblock    Active: active (running) since Tue 2025-02-25 12:48:08 CET; 2 weeks 0 days ago
|_  <hostname>16 hedvighblock    Active: active (running) since Tue 2025-02-25 12:48:08 CET; 2 weeks 0 days ago
hedvigfsc
|_  <hostname>11 hedvigfsc    Active: active (running) since Wed 2025-03-12 08:03:26 CET; 2h 36min ago
|_  <hostname>12 hedvigfsc    Active: active (running) since Mon 2025-03-10 09:29:02 CET; 2 days ago
|_  <hostname>13 hedvigfsc    Active: active (running) since Tue 2025-02-25 13:41:54 CET; 2 weeks 0 days ago
|_  <hostname>14 hedvigfsc    Active: active (running) since Tue 2025-02-25 13:41:54 CET; 2 weeks 0 days ago
|_  <hostname>15 hedvigfsc    Active: active (running) since Tue 2025-02-25 13:41:54 CET; 2 weeks 0 days ago
|_  <hostname>16 hedvigfsc    Active: active (running) since Tue 2025-02-25 13:41:54 CET; 2 weeks 0 days ago
hedvigpages
|_  <hostname>11 hedvigpages    Active: active (running) since Wed 2025-03-12 08:02:52 CET; 2h 36min ago
|_  <hostname>12 hedvigpages    Active: active (running) since Wed 2025-03-12 09:16:09 CET; 1h 23min ago
|_  <hostname>13 hedvigpages    Active: active (running) since Tue 2025-02-25 12:46:40 CET; 2 weeks 0 days ago
|_  <hostname>14 hedvigpages    Active: active (running) since Tue 2025-02-25 12:46:40 CET; 2 weeks 0 days ago
|_  <hostname>15 hedvigpages    Active: active (running) since Tue 2025-02-25 12:46:40 CET; 2 weeks 0 days ago
|_  <hostname>16 hedvigpages    Active: inactive (dead)*
hedvighpod
|_  <hostname>11 hedvighpod    Active: active (running) since Wed 2025-03-12 08:02:32 CET; 2h 37min ago
|_  <hostname>12 hedvighpod    Active: active (running) since Mon 2025-03-10 09:28:58 CET; 2 days ago
|_  <hostname>13 hedvighpod    Active: active (running) since Tue 2025-02-25 12:45:47 CET; 2 weeks 0 days ago
|_  <hostname>14 hedvighpod    Active: inactive (dead)*
|_  <hostname>15 hedvighpod    Active: inactive (dead)*
|_  <hostname>16 hedvighpod    Active: inactive (dead)*
hedvigswatch
|_  <hostname>11 hedvigswatch    Active: active (running) since Wed 2025-03-12 08:02:11 CET; 2h 37min ago
|_  <hostname>12 hedvigswatch    Active: active (running) since Mon 2025-03-10 09:28:37 CET; 2 days ago
|_  <hostname>13 hedvigswatch    Active: active (running) since Tue 2025-02-25 13:40:33 CET; 2 weeks 0 days ago
|_  <hostname>14 hedvigswatch    Active: active (running) since Tue 2025-02-25 13:40:33 CET; 2 weeks 0 days ago
|_  <hostname>15 hedvigswatch    Active: active (running) since Tue 2025-02-25 13:40:33 CET; 2 weeks 0 days ago
|_  <hostname>16 hedvigswatch    Active: active (running) since Tue 2025-02-25 13:40:33 CET; 2 weeks 0 days ago
drivemap
|_  <hostname>11 drivemap    Active: active (exited) since Wed 2025-03-12 09:51:27 CET; 48min ago
|_  <hostname>12 drivemap    Active: active (exited) since Wed 2025-03-12 10:13:36 CET; 25min ago
|_  <hostname>13 drivemap    Active: active (exited) since Tue 2025-02-25 13:41:02 CET; 2 weeks 0 days ago
|_  <hostname>14 drivemap    Active: active (exited) since Tue 2025-02-25 13:40:28 CET; 2 weeks 0 days ago
|_  <hostname>15 drivemap    Active: active (exited) since Tue 2025-02-25 13:27:47 CET; 2 weeks 0 days ago
|_  <hostname>16 drivemap    Active: active (exited) since Tue 2025-02-25 13:20:32 CET; 2 weeks 0 days ago
hedvigdthrottle
|_  <hostname>11 hedvigdthrottle    Active: active (running) since Wed 2025-03-12 09:05:22 CET; 1h 34min ago
|_  <hostname>12 hedvigdthrottle    Active: active (running) since Wed 2025-03-12 09:17:13 CET; 1h 22min ago
|_  <hostname>13 hedvigdthrottle    Active: active (running) since Tue 2025-02-25 13:42:27 CET; 2 weeks 0 days ago
|_  <hostname>14 hedvigdthrottle    Active: active (running) since Tue 2025-02-25 13:42:27 CET; 2 weeks 0 days ago
|_  <hostname>15 hedvigdthrottle    Active: active (running) since Tue 2025-02-25 13:42:27 CET; 2 weeks 0 days ago
|_  <hostname>16 hedvigdthrottle    Active: active (running) since Tue 2025-02-25 13:42:27 CET; 2 weeks 0 days ago
```

#### Check Hedvig Pages after Reboot of a node

```bash
watch -n 30 'echo -n "$(zgrep -i "Loaded Container:" /var/log/hedvig/logs/hblock/system* | wc -l) of "; ls -ld /hedvig/d*/data/* | wc -l; head -2 /tmp/hblock*; tail -2 /tmp/hblock*'
```

#### Check Hedvig Pages after Reboot of the whole cluster

```bash
while true; do clear; echo "=== Check HedvigPages: $(date) ==="; for i in {11..16}; do echo; echo "hostname$i:"; ssh -q hostname$i 'echo -n "$(zgrep -i "Loaded Container:" /var/log/hedvig/logs/hblock/system* | wc -l | sed "s/^/   /") of "; ls -ld /hedvig/d*/data/* | wc -l; head -2 /tmp/hblock* | sed "s/^/   /"; tail -2 /tmp/hblock* | sed "s/^/   /"'; done; sleep 30; done
```
### Check CVFS Version 

#### Check CVFS RPM Version 
```bash
/usr/local/hedvig/scripts/whichCommit.sh
Manifest-Version: 1.0
CommitId: QBD[050ab7206245a9eff4e7fa560eb68433973ff71c: 1.8: 2024-10-2
 5T08:23Z] Duro[6f1837954138dadb66f55c6a13a52dcfeb5bc466: 1.1: 2024-10
 -25T08:21Z] Common[a186650085fae59d305e6a4dac8387ca7744d070: 2024-10-
 25T08:17Z] GMS[3c02a3b360eeda22d1ac368eb33c82d0decf1d37: 2024-10-25T0
 8:20Z] HPOD[ad123f4c89f0c846b4e618ab6a3a018144d660a9:2024-10-25T08:20
 Z] Thrift[6dd89a92284846e1b6a31719cbf7cab9971cb874:2024-10-25T08:19Z]
Branch: QBD[v-5.0.7] Duro[v-5.0.7] Common[v-5.0.7] GMS[v-5.0.7] HPOD[v
 -5.0.6] Thrift[v-5.0.1]
Created-By: Hedvig
Main-Class: com.simontuffs.onejar.Boot
One-Jar-Main-Class: com.quexascale.quexablock.pages.QuexaBlockPagesSer
 vice
```

#### Check CVFS RPM Minor Version 
```bash
rpm -qa | grep hedvig
hedvig-cluster-1.0.0_3806_050ab72062-1.el8.x86_64
hedvig-common-1.0.0_3806_050ab72062-1.el8.x86_64
```

### Monitor Hyperscalex OS upgrade from CLI

#### Connect to control plane
```bash
 tail -f /var/log/commvault/Log_Files/cvupgradeos.log /var/log/commvault/Log_Files/hsupgradedbg/yum.out.log /var/log/commvault/Log_Files/cv_hv_deploy.log /var/log/commvault/Log_Files/cvmanager_ssh.log /var/log/commvault/Log_Files/cvmanager.log
```