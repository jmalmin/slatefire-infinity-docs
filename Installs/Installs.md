 # Installs
**master installs**

The Master server will need basic software installed to allow it to be able to communicate to all node servers. For the most part these installations will be completed as a sudo user and will not make any changes to existing programs on the Centos or Window systems.

**note:**
> **Infinity will run on Windows or Linux systems. Oracle, DB2 and MSSQL databases are supported.**


 1. Install expect for Centos 7 as sudo user.
 
     
		# sudo yum install expect

     
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


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5ODYyODQzODFdfQ==
-->