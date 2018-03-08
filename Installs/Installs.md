 # Installs

## **master installs**

The Master server will need software installed to support the ability for it to communicate to all node servers. For the most part these installations will be completed as a sudo user and will not make any changes to existing programs on the Centos or Window systems.
 
**These will be manual installations on the master server only.** 


----------


**Steps for installs:**

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


 3. Install expect for Centos 7 as sudo user.
 
     
		# sudo yum -y  install expect

     
Or you can compile it from source with these steps:

1) Download the expect package from the below link.

	[http://sourceforge.net/projects/expect/](http://sourceforge.net/projects/expect/)
2) Install the required dependecy packages "Tcl/Tk" language toolkit


       # yum install tcl

3) Install the "expect" package using the below commands
  

       # tar -zxvf expectx.xx.tar.gz
       # ./configure
       # make
       # make install
**Rundeck transfer to master server**

 1. Place rundeck_licensed.tar in the following folder.

		scp rundeck_licensed.tar username@lxcentosmaster:~/repo

 2.  Rundeck port can be configured in the following file:
  `~/apps/start_stop_rundeck.sh`
 

		
		vi ~/apps/start\_stop\_rundeck.sh
		#modify PORT=5550
		PORT=4440 
		# save file 
		Esc
		wq
	`

**JAVA**

 1. Setup Java

    	# add jdk for rundeck

		scp jdk-XXX <username>@<master.server>:~

		# untar and create symbolic link in home directory

		tar -xvzf jdk-8u151-linux-x64.tar.gz

		cd ~

		ln -s jdk1.XXX/ java

		# update ~/.bash_profile

		export JAVA_HOME=~/java
		export PATH=$JAVA_HOME/bin:$PATH
		export PATH

**Rundeck**

 2. Rundeck port can be configured in the following file:
 3. start_stop_rundeck.sh

		start_stop_rundeck.sh

	
		vi start_stop_runeck.sh
		#modify PORT=5550
		PORT=4440 
		# save file 
		Esc
		wq
	

 1. open port for rundeck and make it permanent as root home

	
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
		

 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTY4MjMyOTJdfQ==
-->