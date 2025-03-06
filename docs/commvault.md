# Commvault

## Monitor Hyperscalex OS upgrade from CLI

### Connect to control plane
```bash
 tail -f /var/log/commvault/Log_Files/cvupgradeos.log /var/log/commvault/Log_Files/hsupgradedbg/yum.out.log /var/log/commvault/Log_Files/cv_hv_deploy.log /var/log/commvault/Log_Files/cvmanager_ssh.log /var/log/commvault/Log_Files/cvmanager.log
 ```

