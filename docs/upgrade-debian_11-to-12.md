# Upgrade Debian 11 to 12

## Backup important files

## Check current Linux kernel and Debian version

```bash
cat /etc/debian_version
uname -mrs
```

## Remove all non Debian packages

```bash
sudo apt list '?narrow(?installed, ?not(?origin(Debian)))'
```

## Unhold all packages if any

```bash
sudo apt-mark showhold | more
```

## Update existing packages and reboot the Debian 11 system

```bash
sudo apt update
sudo apt upgrade
sudo apt full-upgrade
sudo apt --purge autoremove
reboot
```

## Updates repositories

```bash
sudo sed -i'.bak' 's/bullseye/bookworm/g' /etc/apt/sources.list
```

## Update the packages index 

```bash
sudo apt update
```

## Prepare for the operating system minimal system upgrade

```bash
sudo apt upgrade --without-new-pkgs
```

## Update Debian 11 to Debian 12 Bookworm

```bash
sudo apt full-upgrade
```

Source: https://www.cyberciti.biz/faq/update-upgrade-debian-11-to-debian-12-bookworm/