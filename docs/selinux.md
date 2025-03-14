# SELinux

## Check config and logs

### Check current mode

```bash
getenforce
Enforcing
```

### List SELinux Contexts for Files and Directories

```bash
ls -Z /bin/ls
system_u:object_r:bin_t:s0 /bin/ls
```

The -Z option shows the SELinux context. In this example:
* system_u: User
* object_r: Role
* bin_t: Type
* s0: Sensitivity level (if applicable)

### Check and search denials 
```bash
ausearch -m avc
```