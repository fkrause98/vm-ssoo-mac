# Operating Systems VM + ARM Mac Setup

<img width="1512" alt="image" src="https://github.com/user-attachments/assets/404439cc-8b53-470e-a0ee-5d30b1fcf64a">


# Versión en español

# ⚠ DISCLAIMER ⚠ #

Esto no esta completamente testeado: Usalo bajo tu propio riesgo

Hay que tener en cuenta, que se hicieron algunos cambios relevantes en este repositorio con respecto a la guía oficial de la cátedra:
- El playbook de Ansible ahora corre `apt update`
- La imagen base de la VM es ahora "cloud-image/ubuntu-20.04". Misma imagen que la original, pero con la arquitectura aarch64 en vez de x86_64
- La materia usa VirtualBox para la VM, pero al momento de escritura de este documento, el soporte para ARM en Mac está en estado beta. Con lo cual usaremos QEMU (usado en Docker para Mac y UTM)


## Dependencias


Probablemente ya lo tengas, pero vamos a necesitar instalar el Homebrew package manager:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```


Una vez que tengamos la Brew, vamos tener que instalar las siguientes dependencias:
```bash
brew install curl ansible qemu
```
y también necesitamos el cast de Vagrant
```bash
brew install --cask vagrant ; export PATH=$PATH:/opt/vagrant/bin
```


Ahora tenemos que agregar el plugin de qemu para Vagrant
```bash
sudo vagrant plugin install vagrant-qemu
```


## File Sharing


Ya que queremos compartir archivos entre el host y la VM, tenemos que habilitarlo [SMB file sharing](https://support.apple.com/en-il/guide/mac-help/mh14107/14.0/mac/14.0).
Cuando se haga, las opciones de la app nos pedirá que introduzcamos una contraseña. La vamos a necesitar para el siguiente paso, así que no te la olvides!


## Creación de VM


Ahora que tenemos todo instalado, vamos a crear y correr la VM

Abri la terminal en el directorio donde se clonó este repositorio y creamos la VM
```bash
cd vm-taller && sudo vagrant up --provider=qemu
```
Aquí también te preguntará la contraseña que insertaste antes para SMB, para el usuario simplemente usar el que el comando `whoami` te diga


Una vez que está todo configurado, el proceso ya está completado. Podemos comprobar que esté todo correctamente hecho entrando mediante SSH a la VM:
```bash
sudo vagrant ssh
```
Tener en cuenta: La VM va estar corriendo en el background constantemente, así que recordar apagarla cuando la terminas de usar
```bash
sudo vagrant halt
```

Si queres arrancar la VM de nuevo, simplemente correr `sudo vagrant up --provider=qemu`.

# English Version

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
