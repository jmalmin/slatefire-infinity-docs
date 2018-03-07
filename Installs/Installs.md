 # Installs
**master installs**

 1. Install expect for Centos 7 as sudo user.
 
     
		# sudo yum install expect

     

Or you can compile it from source with these steps:
1) Download the ecpect package from the below link

	[http://sourceforge.net/projects/expect/](http://sourceforge.net/projects/expect/)
2) Install the required dependecy packages "Tcl/Tk" language toolkit


       # yum install tcl

3) Install the "expect" package using the below commands
  

       # tar -zxvf expectx.xx.tar.gz
       # ./configure
       # make
       # make install


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1Mzk1NzM2NjFdfQ==
-->