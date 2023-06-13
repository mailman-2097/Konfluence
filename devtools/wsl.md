# Introduction

This document will help to setup your work laptop with the tools requried to setup your machine

# Pre-requisites

Local admin access to your windows workstation

# Risks

Please take care in installing various tools on your laptop, the more tools you install the greater the chances of introducing security risks on your laptop and the network.

# Setup your Command line tools

It may be advisable to install packages using various package management tools such as [Chocolatey](https://chocolatey.org/) or [Winget](https://winget.run/) on windows operating systems.

> Please avoid mixing and matching tools to install packages i.e. some with winget and some with chocolatey.

Having access to command line tools is essential for managing cloud infrastructure

## Powershell

Microsoft has released a newer cross platform version powershell which you can install on both windows and linux environments.

It is recommended to install this version of powershell that is not limited to windows. 

[You can review the document linked for further details and installation instructions](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell?view=powershell-7.2)

## Linux Shell 

On windows laptop you can rely on Windows Subsystem for Linux or using a Linux virtual machine through VM player or Virtualbox.

*** Note on Windows Sub System for Linux (WSL) ***

Windows Subsystem for Linux (WSL) lets engineers run bash command-line tools, utilities, and applications -- directly on Windows, unmodified, without the overhead of a traditional VM or dual-boot setup.

You can install and run multiple flavours of Linux distributions such as Ubuntu, Debian, Fedora etc.

## Cloud Shell tools

You can install [Azure Cli](https://github.com/Azure/azure-cli) and the [Azure Powershell](https://github.com/Azure/azure-powershell)  

### Setting up WSL 

> If Microsoft Store is blocked on work laptop, hence you will need to either download the distribution image and manually install it or use the wsl commands.

[Please review this link with instructions to manually install WSL before proceeding](https://docs.microsoft.com/en-us/windows/wsl/install-manual)

```
# Once the distribution is downloaded, run the commands to install the distribution

wsl --install -d Ubuntu-20.04

or

# Latest Ubuntu LTS is only available as manual download. This may install distro name as Ubuntu. You can change the name if you want
Add-AppxPackage .\Ubuntu2204-220620.AppxBundle

# Once the distribution is installed, list them
wsl --list --all

# Set the default distribution if you have more than one installed
wsl --setdefault Ubuntu-22.04

# Launch the instance from terminal or Start Menu
wsl
```

> The default WSL install location is `C:\Program Files\WindowsApps` and there will be additional security restrictions

It is advisable to apply a minimum configuration your WSL instance as follows:

```
sudo vi /etc/wsl.conf

[automount]
root = /
options = "metadata"

# Incase you want to restrict or modify 
# options = "metadata,umask=022,fmask=133"
```

1. The first option in the WSL config mounts `c` drive to WSL Linux root folder as opposed to the default /mnt/
1. The second option enables metadata to maintain the file permission.

[Detailed WSL configuration can be found here](https://docs.microsoft.com/en-us/windows/wsl/wsl-config)

[Another link with some examples](
https://devblogs.microsoft.com/commandline/chmod-chown-wsl-improvements/)

### Changing WSL Distro Name

You can change the WSL Distro Name if you want to identify the version. For this you need eleveted permission to edit registry key. Make sure the wsl instances are shutdown.

```
Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Lxss\{distribution}\DistributionName

```
#### Reboot machine

### Setting Linux VM

You can optionally, setup a local VM through a local hypervisor such as HyperV, VMWare Player, Virtualbox etc. and setup your preferred linux VM.

#### Make life easy with Vagrant

Vagrant is a provisioning tool to configure your Linux VM quick and fast.

```
# The below steps can be used to initialise VM
vagrant init ubuntu/jammy64
vagrant up
vagrant ssh
```

[Link to Ubuntu VM configuration with Vagrant](https://app.vagrantup.com/ubuntu/boxes/jammy640)

You can find additional resources on the internet to learn more about vagrant

## Setting up Git

If you have setup your shell on a Linux VM or WSL. Git should be installed by default. 

```
git config --global user.email "Red.Bull@email.com"
git config --global user.name "Red Bull"
git config --global core.autocrlf input
git config --global core.eol lf
```

#### Create shortcut to onedrive

```
cd ~ 
ln -s "/c/Users/{USERID}/OneDrive" onedrive

```

### Setting up Git on Windows

It may be worthwhile to setup git on windows. This can done from the official git website.

> I have not done git windows setup. So cannot offer much support.

[Git Windows Install](https://git-scm.com/download/win)

Alternatively, you can use a package manager such as [Chocolatey](https://chocolatey.org/)

[Installing Git on Windows through chocolatey](https://community.chocolatey.org/packages/git)

[Installing Github-Desktop on Windows through chocolatey](https://community.chocolatey.org/packages/github-desktop)
> ** Github Desktop is a convenient but one must develop proficiency with the git command line before using this Gui, mistakes made here will be difficult to recover and even wipe out days or weeks of effort **

You need to setup access tokens to authenticate git from command line.
 
[Link to configure git with Azure Devops using SSH](https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=azure-devops#configuration)
> ssh keys are not enabled for Azure Devops so use personal access tokens instead. also ssh-keys may be disabled going forward 
