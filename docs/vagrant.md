# Vagrant

##  Vagrant Quick Start Commands

### Start a VM

```bash
vagrant up
```

### Suspend a VM

```bash
vagrant suspend
```

### Halt a VM

```bash
vagrant halt
```

### Destroy a VM

```bash
vagrant destroy
```

### SSH a VM

```bash
vagrant ssh
```

### Check VM status 

```bash
vagrant status
```

## Boxes

###  Vagrant Quick Start Commands

#### List boxes

```bash
vagrant box list
```

#### Add a box

```bash
vagrant box add ubuntu/trusty64
```

### Update a box

```bash
vagrant box update
```

### Remove a box

```bash
vagrant box remove 
```

## Plugins

### List plugins

```bash
vagrant plugin list
```

### Install plugins

```bash
vagrant plugin install vagrant-vbguest
Installing the 'vagrant-vbguest' plugin. This can take a few minutes...
Installed the plugin 'vagrant-vbguest (0.32.0)'!
```

```bash
vagrant plugin list
vagrant-vbguest (0.32.0, global)
vagrant-vmware-desktop (3.0.4, global)
  - Version Constraint: > 0
```

### Update plugins

#### Update all plugins

```bash
vagrant plugin update
```

#### Update a specific plugin

```bash
vagrant plugin update vagrant-vbguest
```

### Remove a plugin

```bash
vagrant plugin uninstall vagrant-vbguest
```