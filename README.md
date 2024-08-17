# vm-ssoo-mac

Step-by-step guide on how to set up the VM used in FCEyN's  Operating Systems course 
for macOS with an apple silicon chip.

# ⚠ DISCLAIMER ⚠ #

THIS HAS NOT BEEN PROPERLY TESTED 

## Dependencies

You probably already have it, but we'll need to install the home brew package manager:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once we have brew, we'll need to install these dependencies with homebrew:
```bash
brew install curl ansible qemu
```

And we'll need the vagrant cask:
```bash
brew install --cask vagrant
```

## VM Setup

Now that we have everything installed, let's create and run the VM.

Open a terminal wherever you cloned this repo and create the VM:
```bash
cd vm-taller && vagrant up
```

Once everything is set up -- you're done, check everything is in place ssh-ing into the VM:
```bash
vagrant ssh
```

Keep in mind: the VM will keep running in the background, so remember to stop it once you're done using it:
```bash
vagrant halt
```

If you want to start it up again, simply run `vagrant up` again
