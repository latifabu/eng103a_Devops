
# What is DevOps
## Why DevOps?
### Benefits of DevOps

**Four pillars of Devops best practice**
- Ease of Use: Human interaction
- Flexibility: Can add more features
- Robustness - faster delivery of product
- Cost - cost effective, automated process, connect with CI/CD pipelines, faster therefore cheaper.

Monolith , - 2 tier & Microservices Architectures - simple words, within a box that has everything is integrated together, from front end to back end .
To make a change you have to rebuild everything. Microservices are the opposite of a monolith. You have small services that can be deployed individually. Each service has a focus on one aspect of the business functionality. The services work relatively independent of each other and only communicate with the other services when necessary.
![virtualisation-with-vagrant-diagram](https://user-images.githubusercontent.com/98215575/152065728-e5e1dc62-7343-4032-b2e6-a40254fae2a6.png)

--------------------------------------------
 ## How to install a virtual environment (Virtualisation with Vagrant)
  ### 1. First step is to install ruby
 - ```https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.6.6-1/rubyinstaller-devkit-2.6.6-1-x64.exe```
 check ruby version with "ruby --version" in git bash, run as admin
 ### 2. Install Vagrant
 - Then install vagrant with: ```https://www.vagrantup.com/```
 - ```https://www.vagrantup.com/ ```
 - check vagrant version with "vagrant --version" in git bash as admin
### 3. Installing Virtualbox
 - Now install virtual box: ```https://www.virtualbox.org/wiki/Downloads```
 - Virtual box 6.1.32 and click Windows hosts
 - go to  ```C:\Program Files\Oracle\VirtualBox\drivers\vboxdrv```
 - open git bash as admin and enter desired repository
 - Then ```vagrant init ubuntu/xenial64```
 - right click VBoxSup not VBoxDrv.inf 
 - run ```sc start vboxsup``` - in git bash as admin
 - Press the Windows Key and search for Control Panel, go from there to Network and Internet, then Network and Sharing Centre, then Change Adapter Settings.
 - Right click on VirtualBox Host-Only Network and choose Properties
 - Click on Install => Service
 - Under Manufacturer choose Oracle Corporation and under Network Service, choose VirtualBox NDIS6 Bridged Networking dr
### 4. Adding vagrant file
 - `cd` the folder you're running the VM from file 
 - Use nano vagrantfile and add this block of code:
   ```
     Vagrant.configure("2") do |config|

      config.vm.box = "ubuntu/xenial64" 
      # creating a virtual machine ubuntu

      end

    ```
## Launching Vagrant
- Run terminal as admin. `cd` into directory and make sure `Vagrantfile` is in the same folder (the one that holds the `Vagrant` file)
- run `vagrant init`
- `vagrant up`
## Creating a virtual machine ubuntu 
---------------------------------------
## Run your VM
To run the VM, cd into your parent folder (the one that holds the `Vagrant` file) and run `vagrant up`
- check status `vagrant status`
- Run VM `vagrant up`
- `vagrant ssh` to enter your vm
- `Vargrant destroy` deletes vm
- `vargrant halt` to halt vm
- `vagrant reload` to update VM 
-  exit vagrant with `logout`

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
- List dir/files with `ls`
- List all including hidden folders/files
`ls -a`
- Make dir with `mkdir name-of-dir`
- Navigate to dir `cd name-of-dir` (cd \first-letter\+ tab)
- How to create a file `touch <file-name>`
or `nano <file-name>` 
- How to display content of a file ` cat <file-name>`
- To display file content `cat <file-name>`
- How to remove file `rm -rf file-name`
- How to copy file `cp file-destination-name final`
- To move a file enter `mv <file-name><dir-name>`
- Check the running process, enter `top`

### Permissions
- READ Write Executable read only
- How to check permission 
- To check permissions enter `ll`
- To change permissions, enter `chmod <permission-name>`, `sudo chmod +x <file-name>` 
- `sudo chmod +x test.txt` - example of making a file executable 
- Good practice to make the file read only after making it exectable
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
Before deploying software from developers, we need all the dependencies in place in order to run their software.

## Checking Dependencies & Running App
- On local host:

  *-* Open sudo terminal

  *-* Navigate to the environment folder using `cd` and check using `ls` 

  *-* After using `ls` the following files should appear: 

  ``` 
  Genfile Genfile.lock Rakefile 
  ```

  *-* Enter `gem install bundler` , sets up everything for the application containing Gemfile

  *-* Enter `bundle` to install dependencies

  *-* Enter `rake spec` , ruby's method to test for dependencies. Dependancies can be added to the `provision.sh` file so they are installed automatically when the VM is created.

  *-* If any failures are present after entering `rake spec` this can be fixed by installing dependancies

## On a virtual machine:

  *-* `vagrant ssh` to enter the vm

  *-* Start by using `sudo apt-get install nodejs -y` to install nodejs (will not install the latest version of `nodejs` . Will install v4 but v6 is needed)

  *-* `sudo apt-get install python-software-properties` for the python modules

  *-* The code below will install nodejs v6.x
  ```
  curl -sl https://deb.nodesource.com/setup_6.x | sudo -E bash - 
  ```


*-*  Check if the corection version of nodejs by using `sudo apt-get install nodejs -y`

 *-* To install pm2 `sudo npm install pm2 -g`
 

*-* What PM2 does:

``` 
 A production process manager for Node. js applications that has a built-in load balancer. PM2 enables you to keep applications alive forever, reloads them without downtime, and helps you to manage application logging, monitoring, and clustering.
 ``` 

 ## To launch app

 *-* On the local host use `rake spec` to see if all dependencies are installed, this should result in `0` failures
 
 *-*  Now on the virtual machine enter the directory of `app` and from there `ls` and `app$` should be among the listed folders and files.

 *-* Enter the `app$` dir by using `cd`

 *-* Run `npm install` to download the package and its dependencies.(Errors appeared during installation but npm start will run as it intended )

 *-* Now run `npm start`
 
 *-* In your browser enter `http://192.168.10.100:3000/` and `http://192.168.10.100` to see if the program is running. 


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

### Linux variables
- Create Linux Var `FIRST_NAME =LATIF` use caps in linux
- How to check the var with `echo$<KEYANEM>` example, `echo $FIRST_NAME`

### Environment Variables
- How to check `env var`
- command: `printenv key` to print a specific env var or `env` to list all env variables.
- Create env var `export` - to create environment variable the key word is export. 
- `export ABU_NAME=ABU` - env var will be deleted once you exit the VM
- How to make env var persistent?

- In your `.bashrc` file create a persistent variable with `export <VARIABLE_NAME>=<VARIABLE_VALUE>`.
- Then `source ~/.bashrc`to reload the .bashrc file without restarting the VM.
- How to delete `env var`
- Command: `unset <VAR_NAME>` to delete a specific env variable.
- How to `kill` a process in Linux. 
   
   *-* Enter `top` to view all processes. Process ID will be under the PID coloumn.
   *-* Enter `sudo kill <process-ID>`  
- How to use `grep` & | . This commmand is used to find a specific process.
- Example, `env | HOME` 
 
### Reverse Proxy using Nginx
DO NOT UPDATE VM for this exericse.
(Uses http to re-direct traffic to multiple servers)
User's ip is anonymised. Actual proxy is hidden. Below we will hide the port 30003 using reverse proxy. Hidding the port increase security by preventing unnauthorised access to sensitive data.
- This link has a guide for setting up Nginz as a Reverse Proxy Server`https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-16-04`
- Steps prior to step 4 should have been automateda already. Their commands are in the `provision.sh` file.
- Following step 5:

  *-* Working dir is in `app` -> `app`

  *-* After running and listening on localhost.

  *-* Enter the code below in the VM and edit the code:

      
      sudo nano /etc/nginx/sites-available/default
      
  *-* Within the `server` block there will be a `location` block.
Comment out all code within the block.Then add the code below.
Replace `0000` with port number. In this case `3000`.
```
location / {
        proxy_pass http://localhost:0080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
```
  Explaination of the code:
- `proxy_pass` Passes on the request for the port to proxy URL
- `proxy_http_version 1.1;` Sets the HTTP protocol to version 1.1, default version is v1.0
- `proxy_set_header` redefines or appends fields to the request header which is passed to the proxied server.
- `proxy_cache_bypass` caches can interfere with data, bypassing allows correct data to be obtained.

*-* After editing the file, exit and check for errors in nginx by using `sudo nginx -t`.

*-* Restart Nginx with: `sudo systemctl restart nginx`.

*-* Check status with `sudo systemctl status nginx`.


Checking if reverse proxy works at intended
- Change dir with `cd` and enter `app` 
- `ls -a` and then `cd app` 
- `npm install`
- `npm start`
-  App should be running without port 3000 


## Second VM

Step 1 -create 2 VMs -app &db
- Add additional VMs by editing the `vagrantfile`
- Code below launches two VMs (app & db):

```
Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
      app.vm.box = "ubuntu/xenial64"

      #creating private network with ip
      app.vm.network "private_network", ip: "192.168.10.100"
      # Synced app folder   localhost path, path for vm
      app.vm.synced_folder ".", "/home/vagrant/app"
      app.vm.synced_folder "environment", "/home/vagrant/environment"
      # Setting up path for synced folder vm, C+p files from our machine to theirs
      # . means all the files from my current location
      # Provisioning
      app.vm.provision "shell", path: "src/provision.sh"
  end
  # shell = set up(?), run this file
  # provision it, using this method, using this file
  config.vm.define "db" do |db|
      db.vm.box = "ubuntu/xenial64"
      db.vm.network "private_network", ip: "192.168.10.150"
  end
end
```



## Step 2 - setting up mongodb insude the db VM
- DB connection requirement (prerequiste)
- What the dependencies for Mongodb( correct version)
- It should allow access to app
- Database has been set up in our app VM.We want to configure that database on a seperate VM. In this case mongodb. This VM will have all the prequistes that the app VM has plus addition prerequistes needed for mongodb to launch. The app VM and db VM will connect by using the DB_HOST env var. This variable can be found in the dev documentation. The if statement below has been taken from the documentation and will be fufiled if the env DB_HOST is present. The app will use DB_HOST to fetch data from db and display it on "post/index".
````
// connect to database
if(process.env.DB_HOST) {
  mongoose.connect(process.env.DB_HOST);

  app.get("/posts" , function(req,res){
      Post.find({} , function(err, posts){
        if(err) return res.send(err);
        res.render("posts/index" , {posts:posts});
      })
  });
}
````





- change mongo.conf
- /etc/mongod.conf
- by default this mongod.conf
allows 27017 from 127.0.1
271017 from 0.0.0 - allows anyone to access the db
- restart mongo
- enamble mongo
- back to app vm
- create env DB_HOST//:192.168.150.27071:posts

-back to app folder
-npm start

connect the machines using an env called DB_Host
create DB)host 
db ip: 192.168.10.150
export DB_HOST= dp-ip:27017/posts
192.168.10.100/posts
   





