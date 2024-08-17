# Operating Systems VM + ARM Mac Setup

<img width="1512" alt="image" src="https://github.com/user-attachments/assets/404439cc-8b53-470e-a0ee-5d30b1fcf64a">


# ⚠ DISCLAIMER ⚠ #

THIS HAS NOT BEEN PROPERLY TESTED: USE AT YOUR OWN RISK.

Keep in mind, there are some relevant changes made here:
- The ansible playbook now runs `apt update`
- The base box vm is now "cloud-image/ubuntu-20.04", same ubuntu version
  as the original one, but aarch64 instead of x86_64
- The course uses VirtualBox for the VM, but at the time of writing this, support for ARM macs is beta at best; so we'll use qemu instead (used in docker for mac and UTM).

## Dependencies

You probably already have it, but we'll need to install the homebrew package manager:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once we have brew, we'll need to install these dependencies:
```bash
brew install curl ansible qemu
```

And we'll also need the vagrant cask:
```bash
brew install --cask vagrant ; export PATH=$PATH:/opt/vagrant/bin
```

Now we can add the qemu plugin for vagrant:
```bash
sudo vagrant plugin install vagrant-qemu
```

## File Sharing

Since we want to share files between the host and the VM, you'll have to enable [SMB file sharing](https://support.apple.com/en-il/guide/mac-help/mh14107/14.0/mac/14.0).
When you do, the settings app will prompt you for a password, we'll need it for the next step.

## VM Creation

Now that we have everything installed, let's create and run the VM.

Open a terminal wherever you cloned this repo and create the VM:
```bash
cd vm-taller && sudo vagrant up --provider=qemu
```
Here you'll also be asked to input the password you set before for SMB, for user simply use what `whoami` returns

Once everything is set up -- you're done, check everything is in place by ssh-ing into the VM:
```bash
sudo vagrant ssh
```

Keep in mind: the VM will keep running in the background, so remember to stop it once you're done using it:
```bash
sudo vagrant halt
```

If you want to start it up again, simply run `sudo vagrant up --provider=qemu`.
