## Vagrantfile for ASP.NET vNext on Ubuntu

### Introduction
This is a Vagrant file (and .zshrc template) for a Vagrantbox designed specifically for two tasks:

* Develop against the new Microsoft ASP.NET vNext Environment
* Develop a Nodejs application

The base box that has been used is by the lovely folk at boxcutter (https://vagrantcloud.com/box-cutter) who make boxes that works across the various vagrant providers - primarily:
* Oracle's VirtualBox (the default for Vagrant)
* Parallels (get the plugin here https://github.com/Parallels/vagrant-parallels)
* VMWare (you will need a paid plugin for VMWare and Vagrant)

### Current Features

 * Ubuntu 14.04 LTS
 * Mono
 * DNVM
 * nodejs and npm
 * zsh
 * Screen fetch
 * Fortune
 * Htop
 
### Instructions

* Clone Repo
```
git clone https://github.com/shabbirh/VagrantVnext.git
```
* Goto the folder you've cloned the repo to.
* Tear up vagrant
```
vagrant up
```
* The first time you provision the machine may take a longer as a number of archives need to be downloaded.  Following that - as long as you don't destroy the machine - everything should be fast.

Also when using this with ASP.NET vNext - if you want to work on a WebApp - be sure to modify your ``` project.json ``` file.  Add the following:
```
--server.urls http://0.0.0.0:5000
```
to the line that reads
```
"commands": {
    "web": "Microsoft.AspNet.Server.Kestrel"
  },
```

To further simply, the line above should read:
```
"commands": {
    "web": "Microsoft.AspNet.Server.Kestrel --server.urls http://0.0.0.0:5000"
  },
```
if you want to have any sort of remote (or even from your vagrant host to guest) access to an ASP.NET vNext website.

Naturally if you adapt this to proxy via nginx or something like that (which should be the case in any sane production environment, then this step is not and indeed should not be implemented.

### Note
This vagrant file has been tested across the following operating systems and virtualization environments:

* Windows 8.x and 10 with VirtualBox
* Mac OSX 10.11 with Parallels
* Mac OSX 10.11 with VirtualBox