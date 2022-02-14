
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
User's ip is anonymised. Actual proxy is hidden. Below we will hide the port 3000 using reverse proxy. Hidding the port increase security by preventing unnauthorised access to sensitive data.
- This link has a guide for setting up Nginx as a Reverse Proxy Server`https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-16-04`
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


## Step 2 - setting up mongodb inside the db VM
- DB connection requirement (prerequiste)
- What the dependencies for Mongodb (correct version)
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

### Installing dependencies on db VM

Enter the commands below:

`sudo apt-get update -y`
`sudo apt-get upgrade -y`
`sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv D68FA50FEA312927`

```
Downloads the key from keyservers directly into our trusted set of keys.
- apt-key is used to manage the list of keys used by apt to authenticate packages. Packages
which have been authenticated using these keys will be considered trusted.
```
`echo "deb https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list`
```
Registers the repo

```
`sudo apt-get update -y`
`sudo apt-get upgrade -y`
`sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20`

```
Installs the package
```
`sudo nano /etc/mongod.conf`

- Change the bindip in `mongod.conf` from 127.0.0.1 to `0.0.0.0`- allows anyone to access the db. Alternatively,
`sudo sed -i 's/127.0.0.1/0.0.0.0/' /etc/mongod.conf` can be used to change the bindip without having to manually edit the mongod.conf.
- Then `sudo systemctl restart mongod`
- `sudo systemctl enable mongod`
### Connecting app and db VMs
-1 Enter the app VM
-2 Now create the env var DB_HOST by entering: `export DB_HOST=mongodb://192.168.10.150:27017/posts`
-3 Now the `DB_HOST` env var has beem created the if block in app.js will run.
-4 `printenv DB_HOST`
-5 `cd app` -> `cd app`
-6 Then enter `node seeds/seed.js` (Populates the db)
-7 `npm install` then`npm start`
-8 Check `192.168.10.100:3000/posts` 
Issue: After creating DB_HOST the post/ page dispalyed "{}". This was resolved my reloading `vagrant app` and `vagrant db` with using `vagrant reload <VM_name>`.
To make DB_HOST a persistent env var enter these commands in place of steps 2-3:
- `echo "export DB_HOST='mongodb://192.168.10.150:27017/posts'" >> /home/vagrant/.bashrc`
- `source /home/vagrant/.bashrc`
### Automating provisioning of mongodb, app and reverse proxy 

Create a 2nd provision file which was called `provison_db`
The script within `provision_db`
```
 #!/bin/bash
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv D68FA50FEA312927
echo "deb https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
# echo registers repo
sudo apt-get update -y
sudo apt-get upgrade -y 
sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20
sudo sed -i 's/127.0.0.1/0.0.0.0/' /etc/mongod.conf
sudo systemctl restart mongod
sudo systemctl enable mongod

```
- Original provision.sh was changed to:

```
#!/bin/bash

sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install nginx -y
sudo apt-get install nodejs -y
sudo apt-get install python-software-properties -y
curl -sl https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install nodejs -y
sudo npm install pm2 -g
echo "export DB_HOST=mongodb://192.168.10.150:27017/posts" >> /home/vagrant/.bashrc
source /home/vagrant/.bashrc
sudo rm -rf /etc/nginx/sites-available/default
sudo cp app/default /etc/nginx/sites-available/
sudo systemctl restart nginx
sudo systemctl enable nginx

```
Automating the reverse proxy
Created a file called `default` which is referred to when the app is loaded.
Contains the script below:

```
server {

    listen 80;

    server_name _;

    location / {

        proxy_pass http://localhost:3000;

        proxy_http_version 1.1;

        proxy_set_header Upgrade $http_upgrade;

        proxy_set_header Connection 'upgrade';

        proxy_set_header Host $host;

        proxy_cache_bypass $http_upgrade;

    }

}  


```
### Amazon Web Service (AWS)

What is AWS?
- AWS is a cloud platform provided by amazon. It includes infrastrcuture, platform and software as a service.
- AWS offers database storage, compute power and content delivery services for indivduals and businesses.

What is cloud computing?
-Tasks, activties, storage and processes that can be done on your pc or VM can be done on the cloud.
Types of cloud:
- Public clouds
- Private clouds
- Hybrid cloud is increasing popular, hybrid cloud has better security
e.g. banks, some inforation is avaliable, and other are avaliable such as mortgage plans etc.
Confidental work would be on the prvivate server they use a VPN to communicate between server and client.

Benefits of cloud:
- scaliablity
- more reliable and global
- Almost unlimited storage
- Backup and recovery
- APIs
Benefits of AWS:
- services can be used to deploy on aws
- aws exceeds over 1mil active users
- stop spending money running and maintaing data centers
- pay as you go serivce - cost effective
- have cutomer serivce, reply within 24 hours. company account response is 12 hours, enterprise account 1 hour 
- A region in AWS, our region is europe. in one region minimum is 2 activty zones. Multiple avaliablity zones. 
- AWS global infrastrcuture map is always updating. orange regions soon to open. blue, already open. ireland has 3 avaliabilty zones.
  
Why we are able to see different regions interact with each other? So we can select regions that are closest region to the users. when we deploy closer to our user so we can get faster response. BA TEAMS, WE NEED TO KNOW WHO IS GOING to use the product, how many users, when they will use it.Usage times, analysis is needed for scaling. scaling for demand increase.
![My_project_1](https://user-images.githubusercontent.com/98215575/152761094-f26ed835-797f-4644-acfe-7014e979679e.png)

## Launching an instance on using AWS
Here we will launch the app on AWS.
- Log into your AWS account
- Select region Europe-Ireland
- Find the `EC2` service
- Navigate to the `launch instance` drop down menu and click `launch instance`
- Choose an Amazon Machine Image (AMI)
- Search for `Ubuntu Server 18.04 LTS (HVM), SSD Volume Type - ami-07d8796a2b0f8d29c (64-bit x86) / ami-01ddc0aefcdbc53e7 (64-bit Arm)` and select
- Choose an instance type, select the `12 nano` type with `1` vCPUS (can change later)
- Next configure instance details
- Select subnet drop down menu and enter `subnet-0429d69d55dfad9d2|DevOpsStudent default 1a`
- Auto-assign Public IP to `enable`
- Next page, storage page. Do not change anything
- Add tags. Key: `NAME` and value `ENG103A_LATIF`
- Add security group name follwing previous naming convention `ENG103A_LATIF`. Add `ENG103A_LATIF` to description. Due to a mistake my secuirty group name was `launch-wizard-9` but should follow the correct naming convention.
- Set SSH sources to "my ip" and although optional, add "only my ip" to description. NOTE: It is always good to add descriptions.
- Review and launch
- Launch: `choose a new key pair` and enter `key name`

On local host:
- Open terminal as admin
- Download and copy key
- `cd ~/ .ssh`
- `nano <file>.pem`
-  enter content into `<file>.pem`
-  `cat <file>.pem` to check content
-  `chmod 400 <file>pem` to change permissions
-  Go back to AWS copy and then best the below link into the terminal.
-  `ssh -i "<file>.pem" unbuntu@ec2-54-155-213-30.eu-west-1.compute.amazonaws.com:~` - `ssh -i "<file>.pem" unbuntu@<Public IPv4 DNS:~`>.
- enter yes
- You are now in the VM
- run:
 ```
sudo apt update -y
sudo apt upgrade -y
sudo apt install nginx -y
 ```

### Enabling public IP access
- The public IP needs to show on our browser we must configure the security for this to happen.
- On your AWS account navigate to `instances` -> `security` -> `security groups link` -> `edit inbound rules` -> `add rule`:
Enter "HTTP" source: "Anywhere- IPv4 description: "public access"-> save rules.

### Syncing local host files to cloud VM
- `cd ~/.ssh`
- `scp -i "~/.ssh/<file.name> -r app ubuntu@ec2-54-155-213-30.eu-west-1.compute.amazonaws.com` 
- Run:
 ```
sudo apt update -y
sudo apt upgrade -y
sudo apt install nginx -y
 ```
- To enable port 3000
- Return to AWS
  
*-* `instances` -> `security` -> `security groups link` -> `edit inbound rules` -> `add rule`:
"Custom TCP" Port range: "3000" source: "anywhere-IPv4" description: "public access" > save rules

### Creating a second instance for MongoDB
Similarly, to the steps above when we first made an instance.
- Launch an EC2 instance again.
- Follow those steps with these exceptions.
- Add security tags with key being `NAME` AND `ENG103a_name_db`
- Add an extra rule with the following:
   *-* Type: "Custom TCP Rules"

   *-* Port range: 27017

   *-* Source: Anywhere

   *-* Description: allow from app only - (very important as this will allow the application to request information from the db)

- In terminal `~/.ssh`
- `ssh -i "<file>.pem" ubuntu@ec2-<YOUR_IP>.<YOUR_LOCATION>-1.compute.amazonaws.com`
-  `scp -i "~ssh/<file>.pem" -r ~ /eng103a_DevOps/src/provision_db.sh ubuntu@<your_IP>:~` IP on your AWS always changes. Secure copy of eng103a
provision_db.sh.
- This will load `provision_db.sh`
- Enter commands mannually to install mongodb dependencies and change mongo.conf to allow app acess.
- Alternatively, you can load `provision_db.sh` script with:
   
    *-* `sudo chmod +x provision_db_sh`
    
    *-* `sudo ./provision_db_sh`
This will load the already made `provision_db_sh` by giving it permissions and making it executable.
- Once completed `sudo systemctl status mongod` to check if everything has been configured correctly.
- 
### Completion of 2 tier architecture
- Return to AWS and check the app launch status.
- If instance has been stopped, repeat the processes above.
- Enter app vm 
- `cd app`
- Enter the db VM's <Public IPv4 address> (found on aws) into `DB_HOST`.

```
 sudo nano .bashrc
 printenv DB_HOST
 source ~/.bashrc
 printenv DB_HOST
```
To make the DB_HOST env var persistent and executable. 
Then when:
`npm install`
`node seeds/seed.js`
`npm start`

- Load <YOUR_PUBLIC_IP:3000/POSTS> and it should be running.
  
Additional information  
 -  securtiy group will need to allow app instance to access db (only allow app) because its a databse. We do not want any breaches
 - User will interact with app only, if they want to see posts/. app will request the posts page from 
 - If instance do not show 2/2 status check do instance reboot.

### AMI
- Amazon Machine Image/s
- AWS has its own AMI as a service
- It is similar to snapshot in vagrant.
- To create an AMI, select an instance on your EC2 dashboard. Go to actions -> image and templates and click `create image`
- Enter image name as `eng103a_name_ami` 
- Follow the steps when creating a regular instance but adding the security groups from the original instance. Include tab with `name` and `eng103a_name_ami`
- Launch new instance
Terminate old app instance by selecting app instance, `instant state` ->`terminate instance`
-
### Connecting app with DB using AMi instances
- Select instance, click connect, ssh client and then copy example
- Again go back to local host `cd ~/.ssh`
- Open app 
- Paste ssh example if the link has `root` in place of `ubuntu` change `root` to `ubuntu`

Blocker:
Default file had a spacing error between `server_name _` which stopped nginx from activating.
 
```
sudo rm -rf default
sudo nano default

```
Default file was removed and then changed. The standard commands below were then run. 

```
sudo systemctl restart nginx
sudo systemctl enable nginx
npm start
```

After creating and launching your db AMI. ssh into db and change DB_HOST.
DB_host was then changed again because your ip changes daily.
```
 sudo nano .bashrc
 printenv DB_HOST
 source ~/.bashrc
 printenv DB_HOST
```
- After DB_HOST has been saved
- `bash provisions_db.sh` 
- `npm start`

## Amazon Machine Image (AMI)
An AMI is a way to launch a VM on AMS. Similar to snapshot in vagrant an AMI can make a copy of your current instance. Once an AMI is created it can be launched as an instance multiple times.

- To create an AMI:
-> `Select your current instance` -> CLick `actions` -> `Image and templates` ->`create image`
- Enter image name `eng103a_<name>_ami`

### Launching AMIs
- Terminate current instnace which was used to create the AMI.
- Select AMI then -> `create instance from image`
- Following the steps to create a regular instance with the exception of the security groups and the name tag. Use the previously created security group.
Name tag should be `eng103a<name>_from<_instance_name>`
- Launch instance

### Monitoring with CloudWatch
- Select instance in EC2 
- Selecting `monitoring tab` 
- Select `manage detilaed monitoring` and enable (cost extra)
- Click `add to dashboard` and create a `new dashboard`
- Add new CloudWatch window will open.
- Create an alarm following the previous naming convention.
- The alarm should send an sns when the CPU utilisation is >= 25%.
- The CPU_Utilization for our instance was selected.
- The VM was stressed to test our alarm
- Within the VM enter `sudo apt install stress`
- Then `stress -v --cpu 2`

## Auto scaling group(ASG) and Load Balancing


- Run `#!/bin/bash` in your spp instance first
- create a launch instance with the following:
