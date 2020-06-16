# VirtualBox VMs Creation

> Discover Vagrant Boxes [here](https://app.vagrantup.com/boxes/search)

## Supported

| Name | Type | Reference |
|------|------|-----------|
| macOS Catalina | catalina | built on [vagrant box](https://app.vagrantup.com/ramsey/boxes/macos-catalina) |
| macOS Mojave | mojave | built on [vagrant box](https://app.vagrantup.com/ramsey/boxes/macos-mojave) |

## Requirements

Vagrant and VirtualBox are required. Install them running:
```bash
brew cask install virtualbox
brew cask install virtualbox-extension-pack
brew cask install vagrant
brew cask install vagrant-manager # optional
```

## Deploy a VM

### 
Run the following:
```bash
git clone git@github.com:adjogahm/virtualbox-vms.git

VAGRANT_VAGRANTFILE="./virtualbox-vms/template.Vagrantfile" \
  VAGRANT_HOME="~/.vagrant.d" \
  VM_NAME="<VirtualBox VM name>" \
  vagrant up "<Vagrant box (type)>"
```
> For `<`Vagrant box (type)`>` 👉 [Supported](#supported)

### UI Credentials
* Username: vagrant
* Password: vagrant

## Manage your VM boxes

### With vagrant cli [docs](https://www.vagrantup.com/docs/cli)
```bash
vagrant global-status                    # Gets a list of your current Vagrant boxes
vagrant reload [name|id]                 # Reloads a change of config on your Vagrantfile

vagrant ssh [name|id] [-- extra_ssh_args]

vagrant suspend [name|id]                # Suspends the guest machine, rather than fully shutting it down or destroying it
vagrant resume [name|id]                 # Resumes a Vagrant managed machine that was previously suspended
vagrant halt [name|id]                   # Shuts down the running machine Vagrant is managing

vagrant snapshot save [vm-name] NAME     # Saves a new named snapshot
vagrant snapshot restore [vm-name] NAME  # Restores the named snapshot

vagrant destroy [name|id]                # Destroy your VM using an id obtained from `vagrant global-status`
vagrant box remove NAME                  # Delete the box being used to create the VM
```

### With Vagrant Manager
Run `Vagrant Manager.app`

### With VirtualBox
Run `VirtualBox.app` (does not update your user Vagrant configuration though)

### Troubleshooting & Improvements
- If you try to start your VM and it does not boot up at all, check to make sure you have enough RAM to run your VM.
- VirtualBox uses the left command key as the "host key" by default. If you want to use it for shortcuts like `command+c` or `command-v` (copy&paste), you need to remap or unset the "Host Key Combination" in `Preferences -> Input -> Virtual Machine`.
- The default Video Memory of 16MB is far below Apple's official requirement of 128MB. Increasing this value may help if you run into problems and is also the most effective performance tuning.
- If keyboard and mouse do not work inside the VM:
    1. Ensure the [VirtualBox Extension Pack](https://www.virtualbox.org/wiki/Downloads) is installed.
    2. In the VM settings, under `Ports > USB`, select `USB 3.0 (xHCI) Control`.
