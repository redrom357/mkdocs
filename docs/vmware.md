# VMWare

## Misc

### Check if VT-x/AMD-V is Enabled on ESXi Host

```bash
~ # esxcfg-info | grep "HV Support"
         |----HV Support............................................3
            |----World Command Line.................................grep HV Support
```

The table below explains the possible values of HV Support.

| 0 | VT-x / AMD-V support is not available for this hardware. |
| 1 | VT-x / AMD-V might be available on this CPU but it is not supported for this hardware. |
| 2 | VT-x / AMD-V is available but is currently not enabled in the BIOS. |
| 3 | VT-x / AMD-V is enabled in the BIOS and can be used. |


## VMWare Workstation 

### CLI

#### General Commands

#### Power Commands

##### Start a virtual machine with Workstation on a Windows host

```bash
vmrun -T ws start "c:\my VMs\myVM.vmx"
```

##### Stop a virtual machine with Workstation on a Windows host

```bash
vmrun -T ws stop "c:\my VMs\myVM.vmx"
```

##### Reset a virtual machine with Workstation on a Windows host

```bash
vmrun -T ws reset "c:\my VMs\myVM.vmx"
```

##### Suspend a virtual machine with Workstation on a Windows host

```bash
vmrun -T ws suspend "c:\my VMs\myVM.vmx"
```

##### Pause a virtual machine with Workstation on a Windows host

```bash
vmrun -T ws pause "c:\my VMs\myVM.vmx"
```

##### Unpause a virtual machine with Workstation on a Windows host

```bash
vmrun -T ws unpause "c:\my VMs\myVM.vmx"
```

#### Snapshots Commands

##### Creating a snapshot of a virtual machine with Workstation on a Windows host

```bash
vmrun -T ws snapshot "c:\my VMs\myVM.vmx" mySnapshot
```

##### Reverting to a snapshot with Workstation on a Windows host

```bash
vmrun -T ws revertToSnapshot "c:\my VMs\myVM.vmx" mySnapshot
```

##### Deleting a snapshot with Workstation on a Windows host

```bash
vmrun -T ws deleteSnapshot "c:\my VMs\myVM.vmx" mySnapshot
```

#### Guest OS Commands

##### Enabling Shared Folders with Workstation on a Windows host

```bash
vmrun -T ws enableSharedFolders "c:\my VMs\myVM.vmx"
```

##### Running a program in a virtual machine with Workstation on a Windows host with Windows guest

```bash
vmrun -T ws -gu guestUser -gp guestPassword runProgramInGuest "c:\my VMs\myVM.vmx" "c:\Program Files\myProgram.exe"
```