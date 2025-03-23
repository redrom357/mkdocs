# Packer

## Install Packer
Packer Packer may be installed in the following ways:

- Using a precompiled binary.
- Installing from source. (Recommended for advanced users)
- Using your system's package manager.

=== "Install Packer on Ubuntu"

    ```bash
    curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
    sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
    sudo apt-get update && sudo apt-get install packer
    sudo cp /usr/bin/packer /usr/local/bin/packe

    # Validate the Packer Install
    which packer
    /usr/local/bin/packer
    packer version
    Packer v1.10.0

    # Enable autocompletion for Packer CLI
    packer -autocomplete-install
    ```

=== "Install Packer on Mac"

    ```bash
    # Load thrid party repo
    brew tap hashicorp/tap

    # Packer Install
    brew install hashicorp/tap/packer

    # Validate the Packer Install
    packer version
    Packer v1.12.0
    ```

=== "Install Packer on Windows"

    Download binares here: 
    https://releases.hashicorp.com/packer/1.12.0/packer_1.12.0_windows_386.zip

    ```bash
    # Set the path 
    set PATH=%PATH%C:\Program Files\Packer

    # Validate the Packer Install
    $ packer --version
    Packer v1.12.0
    ```
    
## Packer CLI

The Packer command line interface (CLI) is how users/applications interact with Packer.  There is no UI or API for Packer.

### Use the Terraform CLI to Get Help

Execute the following command to display available commands:

```bash
packer -help
```

```bash
Usage: packer [--version] [--help] <command> [<args>]

Available commands are:
    build           build image(s) from template
    console         creates a console for testing variable interpolation
    fix             fixes templates from old versions of packer
    fmt             Rewrites HCL2 config files to canonical format
    hcl2_upgrade    transform a JSON template into an HCL2 configuration
    init            Install missing plugins or upgrade plugins
    inspect         see components of a template
    validate        check that a template is valid
    version         Prints the Packer version
```

Or, you can use short-hand:

```shell
packer -h
```

### Enable autocompletion for Packer CLI

```bash
packer -autocomplete-install
```
#### Enable autocompletion for Packer CLI on Windows with Git Bash

```bash
$ packer -autocomplete-install
## Edit .bashrc file, remove the absolute path andpput this instead:
complete -C packer.exe packer
```

### Subcommands and Flags

```bash
packer validate -h
```

```bash
Usage: packer validate [options] TEMPLATE

  Checks the template is valid by parsing the template and also
  checking the configuration with the various builders, provisioners, etc.

  If it is not valid, the errors will be shown and the command will exit
  with a non-zero exit status. If it is valid, it will exit with a zero
  exit status.

Options:

  -syntax-only           Only check syntax. Do not verify config of the template.
  -except=foo,bar,baz    Validate all builds other than these.
  -machine-readable      Produce machine-readable output.
  -only=foo,bar,baz      Validate only these builds.
  -var 'key=value'       Variable for templates, can be used multiple times.
  -var-file=path         JSON or HCL2 file containing user variables.
```

```bash
packer validate aws-ubuntu.pkr.hcl
```

### Packer fmt

The `packer fmt` Packer command is used to format HCL2 configuration files to a canonical format and style. JSON files (.json) are not modified.  `packer fmt` will display the name of the configuration file(s) that need formatting, and write any formatted changes back to the original configuration file(s).

```bash
packer fmt -diff aws-ubuntu.pkr.hcl
```

If there were formatted changes as a result of running the `packer fmt` command, those changes will be highlighted when specifiying the `-diff` flag.

```
aws-ubuntu.pkr.hcl
--- old/aws-ubuntu.pkr.hcl
+++ new/aws-ubuntu.pkr.hcl
@@ -6,9 +6,9 @@
     filters = {
       name                = "ubuntu/images/*ubuntu-xenial-16.04-amd64-server-*"
       root-device-type    = "ebs"
-    virtualization-type = "hvm"
+      virtualization-type = "hvm"
     }
-        most_recent = true
+    most_recent = true
     owners      = ["099720109477"]
   }
   ssh_username = "ubuntu"
```

### Packer Inspect

The `packer inspect` command shows all components of a Packer template including variables, builds, sources, provisioners and post-processsors.

```bash
packer inspect aws-ubuntu.pkr.hcl
```

```bash
Packer Inspect: HCL2 mode

> input-variables:


> local-variables:


> builds:

  > <unnamed build 0>:

    sources:

      amazon-ebs.ubuntu

    provisioners:

      <no provisioner>

    post-processors:

      <no post-processor>
```

Notice that there are not any variables, provisioners or post-processors in our configuration at this time.  We will be adding those items in future labs.
