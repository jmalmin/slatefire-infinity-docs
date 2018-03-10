## Business process flow

### Product overview

**IPA**

 - IPA software creates a Tririga deliverable that is delivered from the master server to slave servers.  After implementation, IPA will continuously monitor installations, resolve errors, and send notifications to authorized administrators.
 - IPA allows automation of the Tririga installation process and includes more frequent updates to the database.
 - IPA enables rapid deployment of Tririga across multiple servers.
 - Includes the ability to run ad hoc jobs or scheduled jobs using tools such as Rundeck or Jenkins to control the environments from one location.
 - Automation of the installation process using a continuous delivery approach ensures reliably released software at any time and provides the ability to recover from disasters.
 
**OPA**
 - Automated migration of packages from source to destination server(s).
 - Ability to create object migration from database and then trigger export from source Tririga.
 - Export to destination servers and automatic installs are possible.
 - Multiple projects are manually reviewed, if needed, before import in destination server.
 - Updates to OPA are provided for each Tririga Application and Platform version update. 

**Fireball**

 - ØMonitor developer modifications across all objects.
  - Time tracking for developers working in Tririga.
  -  Monitor object customization growth over time which allows forward
   planning.
   - Workflow process monitoring during heavy loads to assess and manage
   performance.
   - Monitor external staging databases.
  -  Reports are generated and emailed to Admins (Excel, Birt, and
   Tableau reports available).
  -  Updates are provided for each Tririga Application and Platform
   version update.

**Infinity**


**Sapphire**

  -  Sapphire reporting reduces the need for multiple query requests.
  -  Our reporting does client side data manipulation.
  -  Users access Tririga system and the values they return are cached in their browser in JavaScript objects.
  -  This allows for decreased chatter between clients and Tririga.
  -  Manipulation of large datasets is done on the clients browser.
  -  Reporting can run alone or as a part of Slate Fire INFINITY
  -  Reports are generated and emailed to Admins (Excel, Birt, and Tableau reports available).
  -  Updates are provided for each Tririga Application and Platform version update.


### Automated Install

 1. Create a master copy of a sample IBM TRIRIGA installation
(“Master Copy”) on the Source VM.


<!--stackedit_data:
eyJoaXN0b3J5IjpbNzQxMzc2OTIzLDEyOTMxOTg0NTJdfQ==
-->