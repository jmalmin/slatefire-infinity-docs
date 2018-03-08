 # Installs

## **master installs**

The Master server will need software installed to support the ability for it to communicate to all node servers. For the most part these installations will be completed as a sudo user and will not make any changes to existing programs on the Centos or Window systems.
 
**These will be manual installations on the master server only.** 


----------


**Steps for installs:**

**SSH**

 1. setup ssh key on master server


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

1) Download the expect package from the below link

	[http://sourceforge.net/projects/expect/](http://sourceforge.net/projects/expect/)
2) Install the required dependecy packages "Tcl/Tk" language toolkit


       # yum install tcl

3) Install the "expect" package using the below commands
  

       # tar -zxvf expectx.xx.tar.gz
       # ./configure
       # make
       # make install

**JAVA**

 1. Setup J

    	# add jdk for rundeck

		scp jdk-8u151-linux-x64.tar.gz <username>@<master.server>:~

		# untar and create symbolic link in home directory

		tar -xvzf jdk-8u151-linux-x64.tar.gz

		cd ~

		ln -s jdk1.8.0_151/ java

		# update ~/.bash_profile

		export JAVA_HOME=~/java

		export PATH=$JAVA_HOME/bin:$PATH

		export PATH

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg2MTE1NTU4OF19
-->