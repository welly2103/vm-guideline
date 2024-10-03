# Basics
## Install virtualbox
https://www.virtualbox.org/

## Install cygwin
https://www.cygwin.com/

## Install Vagrant
https://www.vagrantup.com/

### Create VagrantFile
- Copy the VagrantFile
- Put the file in a directory
- Open up cygwin and fire `vagrant up`

## Connect to the machine
- Use putty or any ssh client and connect with the ip defined in the VagrantFile
- Username and password is `vagrant`

### Install whatever you need from `INSTALL.md`

# Known issues
- `vagrant up` throws provider error. Add `--provider` flag
