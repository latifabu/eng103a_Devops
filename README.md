
# What is DevOps
## Why DevOps?
### Benefits of DevOps

**Four pillars of Devops best practice**
- Ease of Use: Human interaction
- Flexibility: Can add more features
- Robustness - faster delivery of product
- Cost - cost effective, automated process, connect with CI/CD pipelines, faster therefore cheaprer

Monolith , - 2 tier & Microservices Architectures - simple words, within a box that has everything is integrated together, from front end to back end .
To make a change you have to rebuild everything
![virtualisation-with-vagrant-diagram](https://user-images.githubusercontent.com/98215575/152065728-e5e1dc62-7343-4032-b2e6-a40254fae2a6.png)

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
 - Use nano vagrantfile and add this block of code:
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
- `sudo apt-get update -y` Download and install updates
- `sudo apt-get upgrade -y` Upgrades packages that were possibly updated
- `sudo apt-get install nginx -y` <package> install package
- `systemctl status <app> status of specified app`
- `exit`
----------------------------------------
### Linux basics
- Who am I `uname` inside our machine to see our name
- `uname -a` gives more information
- Where am i `pwd` - current directory
- list dir/files with `ls`
- list all including hidden folders/files
`ls -a`
- make dir with `mkdir name-of-dir`
- naviagte to dir `cd name-of-dir` (cd \first-leeter\+ tab)
- how to create a file `touch <file-name>`
or `nano <file-name>` 
- how to display content of the fiile ` cat <file-name>`
- To display file content `cat <file-name>`
- How to remove file `rm -rf file-name`
- How to copy file `cp file-destination-name final`
- To move a file enter `mv <file-name><dir-name>`
- To check running process, enter `top`

### Permissions
- READ Write Executable read only
- How to check permission 
- To check permissions enter `ll`
- To change permissions, enter `chmod <permissionfile-name>`, `sudo chmod +x <file-name>` 
- `sudo chmod +x test.txt` - exmaple of making a file excutable 
- Good practice to make the file read only after making it exectuable
### Bash scripting 
- Let the system know its a bash script by adding `#!/bin/bash` at the top of the document
- Always enter commands below the bash line
- `#!/bin/bash` should be a `.sh` file
- Enter `cat <file>` to view commands inside it
- always run as admin by using `sudo`
- to run type `sudo ./<file-name>.sh`

### /provision.sh 
- add `#!/bin/bash`
- add sudo apt-get update
- add sudo apt-get upgrade
- add sudo apt-get install nginx -y
--------------------
## Environment testing
Before deploying software from developers, we need all the dependancies in place in order to run their software.

## Checking Dependencies & Running App
- On local host:

  *-* Open sudo terminal

  *-* Navigate to the environment folder using `cd` and check using `ls` 

  *-* After using ls the following files should appear: 

  ``` 
  Genfile Genfile.lock Rakefile 
  ```

  *-* Enter `gem install bundler` , sets up everything for the application containing Gemfile

  *-* Enter `bundle` to install dependencies

  *-* Enter `rake spec` , ruby's method to test for dependencies

  *-* If any failures are present after entering `rake spec` this can be fixed by installing dependancies

## On virtual machine:

  *-* `vagrant ssh` to enter the vm

  *-* Start by using `sudo apt-get install nodejs -y` to install nodejs (will not install the latest version of `nodejs` . Will install v4 but v6 in needed)

  *-* `sudo apt-get install python-software-properties` for the python modules

  *-* The code below will install nodejs v6.x
  ```
  curl -sl https://deb.nodesource.com/setup_6.x | sudo -E bash - 
  ```


*-*  Check if the corection version of nodejs by using `sudo apt-get install nodejs -y`

 *-* To install pm2 `sudo npm install pm2 -g`
 

*-* What PM2 does:

``` 
 A production process manager for Node. js applications that has a built-in load balancer. PM2 enables you to keep applications alive forever, reloads them without downtime, helps you to manage application logging, monitoring, and clustering.
 ``` 

 ## To launch app

 *-* On the local host use `rake spec` to see if al dependencies are installed, this should result in `0` failures
 
 *-*  Now on the virtual machine enter the directory of `app` from there `ls` and `app$` should be among the listed folders and files.

 *-* Enter the `app$` dir by using `cd`

 *-* Run `npm install` to download the package and its dependencies.(Errors appeared during installation but npm start will run as it intended )

 *-* Now run `npm start`
 
 *-* In browser enter `http://192.168.10.100:3000/` and `http://192.168.10.100` to see if the program is running. 


 ---------------
 ## Automating updates, upgrades and nginx installtion
The `vagrant up --provision` to running `npm install` can be automated by entering the below code in `provision.sh`

```
#!/bin/bash
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install nginx -y
sudo apt-get install nodejs -y
sudo apt-get install python-software-properties
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install nodejs -y
sudo npm install pm2 -g


```
Code needed to execute the `provision.sh` is in the **Vagrantfile**. Additionally, the code copies all the files (where the vagrant app is present) into the target virtual machine directory

 ```
Vagrant.configure("2") do |config|
  
  config.vm.box = "ubuntu/xenial64" 
  # creating a virtual machine ubuntu
  
  # creating a private network ip
  config.vm.network "private_network", ip: "192.168.10.100"

  # Synced app folder localhost, path for vm
    config.vm.synced_folder ".", "/home/vagrant/app"
                            # . meants everything from current location
  
  #Provisioning
    config.vm.provision "shell", path: "src/provision.sh" 
  
  #Installing 

end
 
 ```








   





