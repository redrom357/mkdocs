# VMWare

## Check if VT-x/AMD-V is Enabled on ESXi Host

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