
# What is devOps
## Why DevOps?
### Benefits of DevOps

**Four pillars of Devops best practice**
- Ease of Use: Human interaction
- Flexibility: Can add more features
- Robustness - faster delivery of product
- Cost - cost effective, automated process, connect with CI/CD pipelines, faster therefore cheaprer

Monolith , - 2 tier & Microservices Architectures - simple words, within a box that has everything is integrated together, from front end to back end .
To make a change you have to rebuild everything

--------------------------------------------
 ## How to install a the virtual environment (Virtualisation with Vagrant)
  ### 1. First step install ruby
 - ```https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.6.6-1/rubyinstaller-devkit-2.6.6-1-x64.exe```
 check ruby version with "ruby --version" in git bash, run as admin
 ### 2. Install Vagrant
 - then install vagrant with: ```https://www.vagrantup.com/```
 - ```https://www.vagrantup.com/ ```
 - check vagrant version with "vagrant --version" in git bash as admin
### 3. Installing Virtualbox
 - Now install virtual box: ```https://www.virtualbox.org/wiki/Downloads```
 - Virtual box 6.1.32 and click Windows hosts
 - go to  ```C:\Program Files\Oracle\VirtualBox\drivers\vboxdrv```
 - open git bash as admin and enter desired repository
 - then ```vagrant init ubuntu/xenial64```
 - right click VBoxSup not VBoxDrv.inf 
 - run ```sc start vboxsup``` - in git bash as admin
 - Press the Windows Key and search for Control Panel, go from there to Network and Internet, then Network and Sharing Centre, then Change Adapter Settings.
 - Right click on VirtualBox Host-Only Network and choose Properties
 - Click on Install => Service
 - Under Manufacturer choose Oracle Corporation and under Network Service, choose VirtualBox NDIS6 Bridged Networking dr
### 4. Adding vagrant file
 - This file needs to be in folder that you're running from the VM
 - Use nano vagrantfile and add thus block of code:
   ```
     Vagrant.configure("2") do |config|

      config.vm.box = "ubuntu/xenial64" 
      # creating a virtual machine ubuntu

      end

    ```
## Launching Vagrant
- Run terminal as admin `cd` into directory and make sure `Vagrantfile` is in the same folder(the one that holds the `Vagrant` file)
- run `vagrant init`
- `vagrant up`
## Creating a virtual machine ubuntu 
---------------------------------------
## Run your VM
To run the VM, cd into your parent folder (the one that holds the `Vagrant` file) and run `vagrant up`
- check status `vagrant status`
- Run VM `vagrant up`
- `vagrant ssh` to enter your vm
- `Vargrant destory` deletes vm
- `vargrant halt` to halt vm
- `vagrant reload` to update VM 

## Unbutu and installing/ updating packages in VM
----------------------
- `sudo apt-get update -y Download and install updates`
- `sudo apt-get upgrade -y Upgrades packages that were possibly updated`
- `sudo apt-get install <package> install package`
- `systemctl status <app> status of specified app`
- `exit`