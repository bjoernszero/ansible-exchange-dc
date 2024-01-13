# Ansible + Vagrant domain controller, exchange server, Office365 client

A example project to setup a Windows Domain Controller and Exchange Server under WSL2/Virtualbox using Vagrant + Ansible

# Getting started

In order to run this project it is required to store the project files on a windows file-system accessible to both WSL2 and the Windows Host, i.e. /mnt/c/Temp. Copy the file contents to any such location and adjust the VAGRANT_WSL_WINDOWS_ACCESS_USER_HOME_PATH environment variable acordingly.

## 1. Prerequisites

Windows 10/11:

- WSL2
- Virtualbox 7

Debian/Ubuntu in WSL2:

- Packages:

```bash
sudo apt install build-essential vagrant ansible python
sudo gem install winrm winrm-elevated
pip install pypsrp --break-system-packages
```

- Vagrant Plugin "virtualbox_WSL2" (vagrant install virtualbox_WSL2)

```bash
vagrant plugin install virtualbox_WSL2
```

- Adjust and use environment when working with vagrant:

```bash
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
export VAGRANT_WSL_WINDOWS_ACCESS_USER_HOME_PATH="/mnt/c/Temp/"
export PATH="$PATH:/mnt/c/Program\ Files/Oracle/VirtualBox"
```

Exchange Server 2019 ISO

- Download the Iso Image from Microsoft and copy to ./iso/
- Adjust the path to the downloaded the ISO image in ./ansible/vars/vars.yml

## 2. Create the domain controller

```
cd vagrant/domain
vagrant up
```

## 3. Create the exchange server

```
cd ../exchange
vagrant up
```

## 4. Create an Office365 machine

```
cd ../client
vagrant up
```
