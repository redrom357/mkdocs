# Packer

## Install Packer
Packer Packer may be installed in the following ways:

- Using a precompiled binary.
- Installing from source. (Recommended for advanced users)
- Using your system's package manager.

=== Install Packer on Ubuntu
```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install packer
sudo cp /usr/bin/packer /usr/local/bin/packe

# Validate the Packer Install
```bash
which packer
/usr/local/bin/packer
packer version
Packer v1.10.0

# Enable autocompletion for Packer CLI
packer -autocomplete-install
```

=== Install Packer on Mac

```bash
# Load thrid party repo
brew tap hashicorp/tap

# Packer Install
brew install hashicorp/tap/packer

# Validate the Packer Install
packer version
Packer v1.12.0
```

=== Install Packer on Windows

Download binares here: 
https://releases.hashicorp.com/packer/1.12.0/packer_1.12.0_windows_386.zip

```bash
# Set the path 
set PATH=%PATH%C:\Program Files\Packer

# Validate the Packer Install
packer --version
Packer v1.12.0
```
