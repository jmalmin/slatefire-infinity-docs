 # Installs

## **Centos 7 Master Server Installs**

The Master server will need software installed to support the ability for it to communicate to all node servers. For the most part these installations will be completed as a sudo user and will not make any changes to existing programs on the Centos or Window systems.
 

> **These following installations are for the master server only.** 

   
   
----------


**Step by Step for each item:**

**Folder Setup**

 1. Master server will need folders setup for applications and local repository.
 2. Folder - apps repo and installs will be created manually.

		cd ~
		mkdir apps repo installs
 
**SSH**

 1. setup ssh key on master server.


		cd ~
		mkdir .ssh
		cd .ssh
		#execute this command and don’t make a passphrase.
		ssh-keygen -t rsa
		cd ~
		chmod -R 700 .ssh

		

**Expect**


 1. Install expect for Centos 7 as sudo user.
 2. If you have access to external repositories please execute the following.
 
     
		sudo yum -y  install expect

     

 3. Or you can compile it from source with these steps:
 4. Download the expect package from the below link.
			[http://sourceforge.net/projects/expect/](http://sourceforge.net/projects/expect/)
 5.  Install the required dependecy packages "Tcl/Tk" language toolkit

	       yum install tcl

 6. Install the "expect" package using the below commands


       tar -zxvf expectx.xx.tar.gz
       ./configure
       make
       make install


**Rundeck Repo transfer to master server**

 1. Place rundeck_repo_final.tar in the following folder.

		scp rundeck_repo_final.tar username@lxcentosmaster:~/repo
		cd ~/repo
		tar-xvf rundeck_repo_final.tar
       
**Rundeck licensed transfer to master server**

 1. Place rundeck_licensed.tar in the following folder.

		scp rundeck_licensed.tar username@lxcentosmaster:~/repo
		cd ~/repo
		cp rundeck_licensed.tar ~/apps
		cd ~/apps
		[username@lxcentosmaster apps]$ ls -al
		total 340104
		drwxrwxr-x.  3 username username        72 Mar  7 20:51 .
		drwx------. 23 username username      4096 Mar  7 20:34 ..
		drwxrwxr-x.  8 username username       149 Mar  7 20:34 rundeck
		-rw-rw-r--.  1 username username 348256681 Feb 28 16:01 rundeck_licensed.tar
		tar-xvf rundeck_licensed.tar


 2.  Rundeck port can be configured in the following file:

		 cd ~/apps/rundeck
		 vi ~/apps/start_stop_rundeck.sh

  

 3. Example modifying port.

		#example:
		#change port from 5550 to 4440
		
		PORT=5550
		PORT=4440 

**Java**

 1. Setup Java

    	# add jdk for rundeck

		scp jdk-XXX <username>@<master.server>:~

		# untar and create symbolic link in home directory

		tar -xvzf jdk-8u151-linux-x64.tar.gz

		cd ~

		ln -s jdk1.XXX/ java

		update ~/.bash_profile

		export JAVA_HOME=~/java
		export PATH=$JAVA_HOME/bin:$PATH
		export PATH

**Rundeck**

 1. Rundeck port can be configured in the following file:
 2. start_stop_rundeck.sh

		
		vi start_stop_runeck.sh
		#modify PORT=5550
		PORT=4440 
		# save file 

	

 3. open port for rundeck and make it permanent as root home.

	
		sudo su
		<provide password>
		[root@masterserver]# firewall-cmd --zone=public --add-port=5550/tcp --permanent
		success
		[root@masterserver]# firewall-cmd --reload
		success`
		cd ~/apps

		#install rundeck in ~/apps folder

		[username@lxcentosmaster rundeck]$ ls -al
		total 97936
		drwxrwxr-x. 8 username username       149 Mar  7 20:34 .
		drwxrwxr-x. 3 username username        79 Feb 28 16:01 ..
		drwxrwxr-x. 2 username username       223 Feb 28 16:01 etc
		drwxrwxr-x. 3 username username      4096 Mar  6 11:59 libext
		drwxrwxr-x. 3 username username        18 Feb 13 23:08 projects
		-rwxrwxr-x. 1 username username 100276613 Feb 10 16:57 rundeck-launcher-X.X.X.jar
		drwxrwxr-x. 9 username username        90 Feb 13 23:06 server
		-rwxrwxr-x. 1 username username      1990 Feb 14 13:12 start_stop_rundeck.sh
		drwxrwxr-x. 4 username username        28 Feb 13 22:57 tools
		drwxrwxr-x. 8 username username       135 Feb 13 23:08 var
		
**Import jobs to rundeck**

 - Please find the latest version of Demo jobs for rundeck in the URL
    provided here. You will import it per the '***Import and archive***' instructions below.		
		[https://slatefirecom.sharepoint.com/:u:/s/SlateFire/EXmVae2wtuVEneRrsqmeFjcB4XQB5az8cyDOcJM0h6qZQQ?e=XXXX](https://slatefirecom.sharepoint.com/:u:/s/SlateFire/EXmVae2wtuVEneRrsqmeFjcB4XQB5az8cyDOcJM0h6qZQQ?e=XXXX)


**Export an archive**
 - To export, visit the "Admin" link in the Rundeck page header.
 - Click on the link under "Export Archive" to download an archive containing the project Jobs, Executions and  -History.
 - This archive can be imported into any other Rundeck project.
 - The archive will contain:
 - All Job definitions from the project All Executions from the project (both Job and Adhoc executions) All Execution log files    (output logs) All History reports from the project Note that the    archive will not contain:
 - The Project config file project.properties located under your $RDECK_BASE/projects/[name]/etc Resource definitions (such as    resources.xml or resources received from external providers.) You    should back up those contents separately if necessary.

**Import an archive**
 - To import the contents of an exported archive, visit the "Admin" link
   in the Rundeck page header.
 - Click on "Import Archive" to display the import form.
 -  Choose the rundeck archive file to import (should end with ".rdproject.jar").
 - Click "Import".
 - The import process:
 - Creates any Jobs in the archive not found in this project with a new unique UUID
 - Updates any Jobs in the archive that match Jobs found in the project (group and name match)
 - Creates new Executions for the imported Jobs, and creates the output log files on disk
 -  Creates new History reports for imported Executions and Jobs
 -  Note that because the archive does not contain the project configuration or resource definitions, you will have to configure
   those separately for the new or updated project.

**Update project nodes in resources.xml**



    cd ~/apps/rundeck/projects/<Your Project Name>/etc
	vi resources.xml
	#edit resources.xml and include your nodes.

 

**Update etc/hosts**


    sudo vi /etc/hosts
    #add ip address and hostname
    #example:
    10.0.0.111 lxcentos1



----------

**Python 3.5.2 install**

 1. Move to the rpm folder inside repo.

	     cd ~/repo/rundeck_repo/linux/python

 2. Install supporting rpm packages.

		yum -y install autoconf-2.69-11.el7.noarch.rpm autogen-5.18-5.el7.x86\_64.rpm automake-1.13.4-3.el7.noarch.rpm gcc-4.8.5-16.el7\_4.1.x86\_64.rpm git-1.8.3.1-12.el7\_4.x86\_64.rpm libmnl-devel-1.0.3-7.el7.i686.rpm libmnl-devel-1.0.3-7.el7.x86\_64.rpm libuuid-devel-2.23.2-43.el7\_4.2.i686.rpm libuuid-devel-2.23.2-43.el7\_4.2.x86\_64.rpm make-3.82-23.el7.x86\_64.rpm pkgconfig-0.27.1-4.el7.i686.rpm pkgconfig-0.27.1-4.el7.x86\_64.rpm zlib-devel-1.2.7-17.el7.i686.rpm zlib-devel-1.2.7-17.el7.x86\_64.rpm expect-5.45-14.el7\_1.x86\_64.rpm ipa-gothic-fonts-003.03-5.el7.noarch.rpm sqlite-devel-3.7.17-8.el7.i686.rpm sqlite-devel-3.7.17-8.el7.x86\_64.rpm xorg-x11-fonts-100dpi-7.5-9.el7.noarch.rpm xorg-x11-fonts-75dpi-7.5-9.el7.noarch.rpm xorg-x11-fonts-cyrillic-7.5-9.el7.noarch.rpm xorg-x11-fonts-misc-7.5-9.el7.noarch.rpm xorg- figlet-2.2.5-9.el7.x86\_64.rpmx11-fonts-Type1-7.5-9.el7.noarch.rpm xorg-x11-utils-7.5-22.el7.x86\_64.rpm yum-utils-1.1.31-42.el7.noarch.rpm figlet-2.2.5-9.el7.x86\_64.rpm

 3. Install python as sudo user.
 
		# move to python folder to install python3.5
		tar xzf Python-3.5.2.tgz
		cd Python-3.5.2
		./configure
		make -j && make altinstall
		
		#Check version of python is installed as normal user : 
		python3.5 -V
		Response should be:  Python 3.5.2


**Pip 3.5 install**

 1. Navigate to pip repo folder. ***Older version of Centos***
 

		cd ~/apps/rundeck_repo/linux/pip
		sudo su
		yum -y install ius-release-1.0-15.ius.centos7.noarch.rpm
		yum -y update
		yum -y install python35u-pip-9.0.1-1.ius.centos7.noarch.rpm python35u-devel-3.5.4-1.ius.centos7.x86_64.rpm
	

 2. **Centos 7** install

	   cd ~/repo/rundeck_repo/linux/pip
	   yum -y install python35u-pip-9.0.1-1.ius.centos7.noarch.rpm
	   
	   or
	   
	   yum -y install python-pip

**Virtualenv install**

 3. Change directory where source code will be run.
 
	    cd ~/apps
	    mkdir rundeck_src
	    cd rundeck_src
	    sudo su
	    pip3.5 install -U virtualenv

 4. verify that you are in the directory where source code will be run on master server
This directory is typically called rundeck_src. or <env name> in example below.


		#run command to create virtual directory
		virtualenv -p python3.5 <env name> 



> Setup complete for Master server

----------

## **Driver Installs**

**DB2**

    cd ~/repo/rundeck_repo/linux/db2/driver
    pip3.5 install ibm_db-2.0.8a0-cp35-cp35m-linux_x86_64.whl


**Selenium**

    cd ~repo/rundeck_repo/linux/selenium
    pip3.5 install selenium-3.8.0.tar.gz

**Chrome**

    cd ~/repo/rundeck_repo/linux/chrome
    sudo su
    ./echo.sh
    yum -y install google-chrome-stable-64.0.3282.167-1.x86_64.rpm
 
**Firefox**

    sudo su
    yum install firefox
**XVFB**

    # virtual desktop for selenium jobs
	# install xvfb for centos
	yum install xorg-x11-server-Xvfb
	xvfb-run --server-args='-screen 0, 1920x1080x16' google-chrome --headless --disable-gpu -remote-debugging-port=9222
	# set export display
	export DISPLAY=:0

**Chrome Selenium Driver**

    cd ~/repo/rundeck_repo/linux/chrome/driver
    sudo su
    yum -y install chromedriver-61.0.3163.100-1.el7.x86_64.rpm
    #setup chrome options on selenium scripts to include (no-sandbox) if fails on load
    
**Phantomjs**

	# virtual desktop
	# download phantomjs
	phantomjs-1.9.8-linux-x86_64.tar.bz2
	sudo mkdir -p /opt/phantomjs
	sudo tar -xjvf phantomjs-1.9.8-linux-x86_64.tar.bz2 --strip-components=1 -C /opt/phantomjs/
	sudo ln -s /opt/phantomjs/bin/phantomjs /usr/bin/phantomjs
	#Test
	phantomjs /opt/phantomjs/examples/hello.js

**Geckodriver**

    # virtual desktop
	[username@vm1]$ cd /usr/local/bin/
	[username@vm1 bin]$ ls
	[username@vm1 bin]$ sudo tar -xvzf ~/geckodriver-v0.17.0-linux64.tar.gz
	[sudo] password for username:
	geckodriver
	[username@vm1 bin]$ sudo chown root:root geckodriver
	[username@vm1 bin]$ ll
	total 6972
	-rwxrwxr-x. 1 root root 7136049 Jun 9 17:47 geckodriver

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MTY2Njc0MzhdfQ==
-->
