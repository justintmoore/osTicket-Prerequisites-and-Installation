<p align="center">
    <img src="https://i.imgur.com/Clzj7Xs.png" alt=osTicket logo"/>  
    
Sorry about the change in format. As I continue to document my projects, I'm always looking for better ways to enhance my presentations! 
    
## Tools, Utilities, Services Used
- Microsoft Azure <br>
- Remote Desktop <br>
- Internet Information Service


## Environments Used
- Windows 10 <br>
- Windows Server 2022
  

## Program Walkthrough
<p align="center">
    Once the Windows 10 VM has been set up in Azure, log into the machine with your credentials. It is best to create a notepad and save a copy of any credentials used along the way for this lab, as there'll be many.
Within the VM, open the Microsoft Edge web browser and download <a href="https://drive.usercontent.google.com/download?id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD&export=download&authuser=0">osTicket Installation Files</a>. Extract the files and you should see the following.
</p>
<br>

<p align="center">
    Create a Virtual Machine, during this process you will be prompted to create a resource group. Ensure that your machine has at least 2vCPUs, and 8GB of RAM. Choose your admin account credentials. In previous walkthroughs we would create a virtual network, but today we will allow azure to create one for us. Everything else we will leave alone. Review and Create VM. Once complete, search for your virtual machine and get the public IP
</p>
<p align="center">
    <img src="https://i.imgur.com/7E68pjp.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   Now we will use Remote Desktop Protocol (RDP) to remote into our virutal machine. ACL prompt will pop up, enter your created credentials.
</p>
<p align="center">
    <img src="https://i.imgur.com/ZvJKB9h.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   Open up your Microsoft Edge browser. We will open the "osTIcket-Installation-Files.zip" folder and download it.
</p>
<p align="center">
    <img src="https://i.imgur.com/avEYg0I.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
    Open up the download folder, right click and select "Extract All", and place it on your VMs desktop, and press next.
</p>
<p align="center">
    <img src="https://i.imgur.com/Jc6x4wK.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   We will now Enable IIS. IIS stands for Internet Information Services, it's basically a web server that will run on this VM, enabling us to run osTicket. In a browser, go to the URL and type the localhost address. Localhost address is 127.0.0.1. You should see an error message informing you that it refused to connect.  
</p>
<p align="center">
    <img src="https://i.imgur.com/BnaW0Y3.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   To enable IIS, taskbar search bar, and go to control panel -> Programs ->Programs and Features -> Turn Windows features on or off -> Internet Information Services, and check the box. Then expand "World Wide Web Services" and expand "Application Devlopment Features", and check "CGI". Press ok. ( Takes some times, just wait)    
</p>
<p align="center">
    <img src="https://i.imgur.com/5FULbbi.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   Now that it's finished, go back to your browser and reload the url 127.0.0.1. There will be something on the screen, which is the default webpage for your VMs web page.    
</p>
<p align="center">
    <img src="https://i.imgur.com/ptQcBvK.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   From the osTicket Installation Files on the desktop we are going to install PHP Manager for IIS (PHPManagerForIIS_V1.5.0). PHP is a backend language used in alot of webservers. PHP Manager ensures PHP is correctly configured to run IIS.    
</p>
<p align="center">
    <img src="https://i.imgur.com/kv1ePr0.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   Click it to install, say yes and agree to everything. From within the same folder we will install the Rewrite Module, rewrite_amd64_en-US. The Rewrite Module facilitates URL rewriting and redirect users to URLs. Say yes to everything.  We will now create a directory on the C Drive. In your file explorer, go to Windows(C:) -> and Create folder named "PHP".
</p>
<p align="center">
    <img src="https://i.imgur.com/Ta30FID.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   We can now unzip "PHP 7.3.8" from the osTicket Installation Files to the "C:\\PHP" directory we just created.
</p>
<p align="center">
    <img src="https://i.imgur.com/cd3vjAF.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   Install "VC_redist.x86" from osTicket Installation Files. This is C++ redistributables and osTicket relies on libraries that are part of Microsoft Visual C++ and ensures the program runs smoothly. From from osTicket Installation Files install "MySQL-5.5.62-win32". Simply, its just a database to store user accounts, tickets, etc. For MySQL, we will do a "typical setup" -> after installation launch MySQL and click finish. Configurations Wizard will pop up (after install), choose "standard configuration and click next. Leave the next page as is, and click next again. At this point you should be on this page. Be careful here, do not mess things up!
</p>
<p align="center">
    <img src="https://i.imgur.com/kwsCmQL.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   Choose a root password, and confirm your password again. For the sake of this project choose something simple. Click next, and select "execute". Next, we will open IIS as an admin. Search "IIS" from task search bar and open as admin.
</p>
<p align="center">
    <img src="https://i.imgur.com/7ali1kY.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   We need to register PHP from within IIS (PHP Manger -> C:\PHP\php-cgi.exe). Basically telling the webserver the existence of PHP, and where it's located.  To do this open PHP Manager, and slect the link "Register new PHP version.
</p>
<p align="center">
    <img src="https://i.imgur.com/dVRM4LT.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center">
   We will put in the path of the PHP folder we created on the C drive prior, "C:\PHP\php-cgi.exe". Now that we have registered PHP within IIS, we must stop, and start IIS for this to take affect. On the left hand side we can see osticket-vm" under the connections window, right click that and choose stop. Wait for bit, then right click again and choose start. Minimize your IIS screen and make your way back to the osTicket Installation Files. Our next step is installing osTicket. To install osTicket, we must extract "osTIcket-v1.15.8", to our current folder. Open the osTicket folder, and copy the "upload" folder into "C:\inetpub\wwwroot" which is the root of the webserver.
</p>
<p align="center">
    <img src="https://i.imgur.com/B5nCp3V.png" height="60%" width="60%" alt="step one"/>
</p>
<br>



<p align="center"> 
   Once the folder is copied over, right click the "upload folder" and select "rename". We will rename it to "osTicket". Maximize IIS, and stop/start the server again! We will attempt to access the site by going to sites -> Default Web Site -> os Ticket -> Browse *.80 (http).
</p>
<p align="center">
    <img src="https://i.imgur.com/aGXVzSs.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center"> 
   You should see the osTicket Installer page.
</p>
<p align="center">
    <img src="https://i.imgur.com/AF1tYqR.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center"> 
   Notice that there are some extensions that are not enabled, lets see if we can fix that. Go back to IIS -> Default -> osTicket. Double click PHP Manager, click "enable or disable extensions", and enable the following: php_imap.dll, php_intl.dll, php_opache.dll. The php_imap.dll, php_intl.dll, and php_opcache.dll extensions in osTicket enable email fetching via IMAP, support for multiple languages, and improved PHP performance through caching, respectively, when configured in IIS.
</p>
<p align="center">
    <img src="https://i.imgur.com/3stLRVC.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center"> 
   After enabling the extensions, go to your brwoser and refresh, your should notice your page has updated your recommended exentions.
</p>
<p align="center">
    <img src="https://i.imgur.com/5HaD22y.png" height="60%" width="60%" alt="step one"/>
</p>
<br>



<p align="center"> 
  Moving along, we must change our "C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php", to "C:\inetpub\wwwroot\osTicket\include\ost-config.php".
</p>
<p align="center">
    <img src="https://i.imgur.com/DlcMaPd.png" height="60%" width="60%" alt="step one"/>
</p>
<br>



<p align="center"> 
 We must now assigm permissions to "ost-config.php". We do this by right clicking "ost-config.php" -> properties -> Security -> Advanced. I will select "Disable Inheritance" to strip away all inherited permissions. This leaves us with non permissions
</p>
<p align="center">
    <img src="https://i.imgur.com/ZB7Wug5.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center"> 
 Now to set up new permissions we click Add -> Select Principal -> in the text box type everyone -> click ok -> lastly click Full Control. (I understand that it's bad practice to give everyone full permissions, I was unsure of the default account osTicket assigned to us). It should look like this...
</p>
<p align="center">
    <img src="https://i.imgur.com/SIIANb2.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center"> 
 Click Apply -> click Ok. This gives osTicket full control to the configuration file (in this case everyone, in a production environment it would be the admin). Go back to your browser, and click continue. Fill out the osTicket Basic Install information, stopping at Database settings. We created our database on the backend, but we need to login and create another database specific for osTicket then provide the credentials. 
</p>
<p align="center">
    <img src="https://i.imgur.com/oGBT4If.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center"> 
 To do this we must go back to our osTicket Installation Files, and install "HeidiSQL", which is a GUI used to access MySQL (and also MariaDB, PostgreSQL, and SQL Server) databases.
</p>
<p align="center">
    <img src="https://i.imgur.com/LixEVbd.png" height="60%" width="60%" alt="step one"/>
</p>
<br>



<p align="center"> 
 Aceept agreements, and next all the way through, install, click finish, and skip. You should now see the session manager. 
</p>
<p align="center">
    <img src="https://i.imgur.com/ncuX75S.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center"> 
 We need to setup a connection to our database, and then setup a database for osTicket to use. On the bottom left click new, and enter your MySQL credentials you setup prior for the user and password. Now click open. This opens up a connection to our database. To create a osTicket database go to the underlined dolphin -> Create new -> Database
</p>
<p align="center">
    <img src="https://i.imgur.com/QRvLxEi.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center"> 
 Name the Database "osTicket", and click ok. If you look at the left column, you will see the database you just created. We will now move on to the browser and continue setting up osTicket. Fill is Database Settings with teh applicable information, and click install now.
</p>
<p align="center">
    <img src="https://i.imgur.com/X4Peywk.png" height="60%" width="60%" alt="step one"/>
</p>
<br>


<p align="center"> 
 If everything was done correctly we have successfully setup osTicket, and all it's dependencies!
</p>
<p align="center">
    <img src="https://i.imgur.com/U5ydMYd.png" height="60%" width="60%" alt="step one"/>
</p>
<br>

## Lessons Learned
<p align="center">
    This lab taught me some things, while I may not see as important, it's nice to know. I learned about Internet Information Services (IIS) and how is it web server software used by Microsoft to host and manage websites, applications, and services on Windows Servers. This is the first time I ever heard, let along put hands on IIS. I learned that is requires quite a bit of dependencies to function. I got the lesson that PHP is a server-side scripting language that allows a person to create dynamic and interactive websites. This is my first experience with PHP as well, as a cybersecurity practitioner, I understand the importance of understanding PHP. I got more hands on experience installed MySQL, which is just a database we used for osTicket, and HeidiSQL which is an GUI allowing us to interactive with MySQL databases. We used HeidiSQL, to create a database within the already established MySQL database to store osTicket resources. What I can further learn is the configurations that go along with PHP and osTicket. 
</p>
<br>
<p align="center">
    <strong>The Marathon Continues!</strong>
</p>



























<!--

<br>

<p align="center">
   Below is the admin portal, where we have control over settings and configurations.
</p>

<br>

<p align="center">Admin Portal</p>
<p align="center">
    <img src="https://i.imgur.com/yIvgXvG.png" height="60%" width="60%" alt="step one"/>
</p>

<br> 

<p align="center">End User Portal</p>
<p align="center">
    <img src="https://i.imgur.com/A2xk8gp.png" height="60%" width="60%" alt="step one"/>
</p>
<br>

<p align="center">The first thing we are going to do is configure roles, which in short is group users together based on job duties and function, and setting permissions to those created groups. To do this we must navigate Admin Panel -> Agents -> Roles. Here we can do a number of things, such as check the preconfigured roles and permissions, or you can add new roles. In this case click the button Add New Roles. It's good to mention that naming scheme may differ amongst the different ticketing services, it's typically the same in functionality.
</p>

<p align="center">
    <img src="https://i.imgur.com/Ei2ncZT.png" height="60%" width="60%" alt="step one"/>
</p>
<br>

<p align="center">
    Now we go into Permissions, and assign permissions based on Tickets, Tasks, and Ability to manage the Knowledgebase. Now select Add Role. Of course you are going to be specific to a persons actual job responsibilities, here we are just having a little fun. 
</p>

<p align="center">
    <img src="https://i.imgur.com/H8zul82.png" height="60%" width="60%" alt=""/>
</p>
<br>

<p align="center">
    Next we will configure departments (Help Desk, Interns, SysAdmins, Networking).
    To do this we must navigate to Admin Panel -> Agents -> Departments.
    We will add a new department in the shape of SysAdmins.
    There are many different configurations we can do, such as choosing specific SLA's, creating agents, etc. Much of this will be covered later in this project. For now, we will set the Parent, name, then select Create!
</p>

<p align="center">
    <img src="https://i.imgur.com/xrR7BDr.png" height="60%" width="60%" alt="step one"/>
</p>
<br>

<p align="center">
    Next we will create Teams. Teams is an entity where you can add different agents, from different departments, with different roles. To configure a Team navigate to Admin Panel -> Agents -> Teams. For my example I chose to name the Network Troubleshooting team. While we don't have any agents yet, This can consist of a network engineer, IT support specialist, and a sysadmin. Create your Team.
</p>

<p align="center">
    <img src="https://i.imgur.com/kb79kpR.png" height="60%" width="60%" alt=""/>
</p>
<br>

<p align="center">
    We must configure osTicket in a way that allows anyone to create tickets even if they aren't registered in the system. This includes End Users. To do this navigate to Admin Panel -> Settings -> User Settings (UNCHECK Registration Required)
</p>

<p align="center">
    <img src="https://i.imgur.com/FwZCMom.png" height="60%" width="60%" alt=""/>
</p>
<br>

<p align="center">
    We can now work on creating Agents. Navigate to Admin Panel -> Agents -> Add New Agent. Creating Agents is straight forward, you can set passwords (statically, or at next login), choose departments, roles, teams, etc. I will go ahead and creat a couple Agents, it's a good idea to mark them down in a text editor for future lab use.
</p>

<p align="center">
    <img src="https://i.imgur.com/KHJa5wl.png" height="60%" width="60%" alt=""/>
</p>

<p align="center">
     <img src="https://i.imgur.com/bNChVf9.png" height="60%" width="60%" alt=""/>
</p>
<br>

<p align="center">
    Now that we created Agents, it's time to create of End Users! Navigate to Agent Panel -> Users -> Add User. Compared to creating Agents, it's much simpler.
</p>

<p align="center">
     <img src="https://i.imgur.com/rXu1gtn.png" height="60%" width="60%" alt=""/>
</p>
<br>

<p align="center">
    Service Level Agreements or SLA for short. These are formal agreements between a service provider and a client that defines the expected service standards, such as response times, resolution times, and performance metrics, ensuring accountability and clarity for both parties. To create SLAs navigate to Admin Panel -> Manage -> SLA -> Add New SLA Plan.
</p>
<p>
    I will create 3 SLAs based on severity levels, A being the worst, and C being everyday ticket on low priority. If you need definitions of each field name, hover over the question mark. For an Example I have Sev-A, for Severity A. A Grace Period of 1 hour of receiving the ticket, in a 24/7 schedule. So it has to be resolved within an hour of being created. We will leave everything else blank.
</p>

<p align="center">
     <img src="https://i.imgur.com/7q4IwAY.png" height="60%" width="60%" alt=""/>
</p>
<br>

<p align="center">
    Lastly we will configure Help Topics. These will help categorize tickets such as password resets, networking issues, hardware issues, equipment requests, etc. Navigate to Admin Panel -> Manage -> Help Topics -> Add New Help Topic
</p>

<!--
<p align="center">
    <img src="https://github.com/user-attachments/assets/f0799a35-207d-45f8-9e7e-21fa5686f488" height="60%" width="60%" alt=""/>
</p>

<p align="center">After creating a virtual machine in azure and logging in. Download and unzip the osTicket installation files.</p>

<p align="center">
    <img src="https://github.com/user-attachments/assets/1e5dab0f-bf89-43d1-97d4-6a5ff60a2ff2" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Enable IIS in windows by following these steps: control panel -> windows features -> world wide web -> application development features -> CGI. To know this has worked is by doing a loopback address. In the browser type in 127.0.0.1. If you see a blue screen it has worked. If you see an error, then go back through the steps previously.</p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/b6d885ad-42dc-47fd-8215-d033ac849013"
 height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Install PHP manager and Rewrite Module. </p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/5617ec01-fae2-49cb-92b8-9b0531cc97be" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Go to files -> windows C: and create a directory named C:\PHP. </p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/b31cb80e-e719-4d78-98a0-e2a99d4178b7" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Unzip PHP 7.3.8 into the created directory. </p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/8e7bb78d-377f-4f6f-8f12-9226f15b04a3" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Install VC and MySQl.</p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/39b08ee7-4aaa-4203-9843-0cbd16b50bc2" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Set up MySQl by selecting Typical Setup -> launch configuration -> Standard Configuration -> type in an username and password.</p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/273c5dc1-6a08-43b1-9a2a-0f854542775f" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Open IIS as Admin.</p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/0cabe267-164a-4c5e-a63e-83af30e249c8" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Click on PHP manager and click register. Select php-cig.exe from the C:\PHP folder. And reload IIS.</p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/52c397b0-b1dd-4b4d-a6ec-f82a66fa5a42" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">In folders, unzip osTicket install files. Copy uploads into c:\inetpub\wwwroot and rename to osTicket.</p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/766b96b6-2d27-43ac-98e5-8461f86f8b05" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Reload IIS again and right click Browse *:80. This should open osTicket into the browser. If this did not happen then review the previous steps.</p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/859cf37d-12dd-44f2-a435-86109a8f6bb1" height="50%" width="50%" alt="step one"/>
</p>

<p align="center"> For osTicket to work these extensions should be enabled: php_imap.dll, php_intl.dll, php_opcache.dll. Refresh the browser and the x's shown should be green checks.</p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/0bc5db5e-b7a0-4481-b5bc-3ff77768298b" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Rename ost-smapleconfig.php to ost-config.php.</p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/a2fd8fe0-a5be-4e74-b082-0782fd12b591" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Right click ost-config.php, select properties, and select security. Here change permissions to everyone.</p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/926dfad7-f5d8-491a-9126-6da0832b51da" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">By now you should be on the set up page of osTicket; name, password, and email should be already placed in. In the bottom section will need a database file from Heidi SQL. Install Heidi SQL from the osticket install files folder. Create a new session, log in with the user and password created from MySQL. Connect to the session and create a database osTicket. Once the bottom section is filled out click continue.</p>

<p>
<p align="center">
    <img src="https://github.com/user-attachments/assets/b9e886dc-1efa-4ee5-bb1e-c2f0b37c15aa" height="50%" width="50%" alt="step one"/>
</p>

<p align="center">Congrats you have downloaded osTicket. From here you can learn the program and how to resolve tickets and create accounts.</p>









<!--

<p align="center">
    <img src="https://i.imgur.com/Clzj7Xs.png" alt=osTicket logo"/>
  
## osTicket - Prerequisites and Installation
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

## Operating Systems Used 

- Windows 10 Pro </b> (22H2), at least 2vCPUs, 8GB RAM

## List of Prerequisites

- <b>PHP manager for IIS</b> - ensures PHP is correctly configured to run IIS
- <b>Rewrite module </b> - facilitates URL rewriting and redirect users to URLs
- <b>VC_redist.x86</b> (redistributable) - osTicket relies on libraries that are part of Microsoft Visual C++ and ensures the program runs smoothly
- <b>MySQL</b> - for storing data into databases
- <b>HeidiSQL</b> - interface for accessing MySQL 


## Installation Steps  
<p>
Once the Windows 10 VM has been set up in Azure, log into the machine with your credentials. It is best to create a notepad and save a copy of any credentials used along the way for this lab, as there'll be many.
Within the VM, open the Microsoft Edge web browser and download <a href= https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD>osTicket-Installation-Files.zip</a>. Extract the files and you should see the following.
</p>


- Create a Virtual Machine, during this process you will be prompted to create a resource group. Ensure that your machine has at least 2vCPUs, and 8GB of RAM
- Choose your admin account credentials
- In previous walkthroughs we would create a virtual network, but today we will allow azure to create one for us. Everything we will leave alone
- Review and Create VM. Once complete, search for your virtual machine and get the public IP
  ![1](https://github.com/user-attachments/assets/a56a18fa-98e7-4191-af2a-09ee57c1883d)
- Now we will use Remote Desktop Protocol (RDP) to remote into our virutal machine.
- ACL prompt will pop up, enter your created credentials.  
  ![1](https://github.com/user-attachments/assets/76f2323d-8080-41c7-85b7-2df9ce3e36ce)
- Open up your Microsoft Edge browser 
- We will open the "osTIcket-Installation-Files.zip" folder and download it  
  ![1](https://github.com/user-attachments/assets/0d761a62-cca1-4370-b9fc-78ec6cb898ed)
- Open up the download folder, right click and select "Extract All", and place it on your VMs desktop, and press next
  ![1](https://github.com/user-attachments/assets/255f2355-8758-46a8-aa4f-00b7c0794b4d)  
- We will now Enable IIS. IIS stands for Internet Information Services, it's basically a web server that will run on this VM, enabling us to run osTicket
- In a browser, go to the URL and type the localhost address. Localhost address is 127.0.0.1. You should see an error message informing you that it refused to connect  
  ![1](https://github.com/user-attachments/assets/476e63af-a9f7-4a54-8301-ea9c10b14b14)  
- To enable IIS, taskbar search bar, and go to control panel -> Programs ->Programs and Features -> Turn Windows features on or off -> Internet Information Services, and check the box. Then expand "World Wide Web Services" and expand "Application Devlopment Features", and check "CGI". Press ok. ( Takes some times, just wait)  
  ![1](https://github.com/user-attachments/assets/c2964312-470d-43e0-9806-3092b1bb0ad3)  
- Now that it's finished, go back to your browser and reload the url 127.0.0.1. There will be something on the screen, which is the default webpage for your VMs web page.
  ![1](https://github.com/user-attachments/assets/211e9515-f929-471c-83d6-384d86cdac0d)
- From the osTicket Installation Files on the desktop we are going to install PHP Manager for IIS (PHPManagerForIIS_V1.5.0). PHP is a backend language used in alot of webservers. PHP Manager ensures PHP is correctly configured to run IIS.
  ![1](https://github.com/user-attachments/assets/ba042dd5-9288-4903-a306-92440401075d)
- Click it to install, say yes and agree to everything.
- From within the same folder we will install the Rewrite Module, rewrite_amd64_en-US. The Rewrite Module facilitates URL rewriting and redirect users to URLs. Say yes to everything.
- We will now create a directory on the C Drive. In your file explorer, go to Windows(C:) -> and Create folder named "PHP"
  ![1](https://github.com/user-attachments/assets/929082b7-8007-4960-b583-9a07eb55c3d9)
- We can now unzip "PHP 7.3.8" from the osTicket Installation Files to the "C:\\PHP" directory we just created.
  ![1](https://github.com/user-attachments/assets/d2ac0329-e9e1-4b3b-b3ac-63deed2835c3)
- Install "VC_redist.x86" from osTicket Installation Files. This is C++ redistributables and osTicket relies on libraries that are part of Microsoft Visual C++ and ensures the program runs smoothly
- From from osTicket Installation Files install "MySQL-5.5.62-win32". Simply, its just a database to store user accounts, tickets, etc.
- For MySQL, we will do a "typical setup" -> after installation launch MySQL and click finish
- Configurations Wizard will pop up (after install), choose "standard configuration and click next. Leave the next page as is, and click next again.
- At this point you should be on this page. Be careful here, do not mess things up!
  ![1](https://github.com/user-attachments/assets/123eb807-9855-412f-97fe-4a44ce6c5505)
- Choose a root password, and confirm your password again. For the sake of this project choose something simple. Click next, and select "execute"
- Next, we will open IIS as an admin. Search "IIS" from task search bar and open as admin
  ![1](https://github.com/user-attachments/assets/2582380b-3a6e-499b-9f7a-3a92df20638c)
- We need to register PHP from within IIS (PHP Manger -> C:\PHP\php-cgi.exe). Basically telling the webserver the existence of PHP, and where it's located.  To do this open PHP Manager, and slect the link "Register new PHP version
  ![1](https://github.com/user-attachments/assets/f9f21817-8aa9-4621-ac78-8e6a40da2385)
- We will put in the path of the PHP folder we created on the C drive prior, "C:\PHP\php-cgi.exe". Now that we have registered PHP within IIS, we must stop, and start IIS for this to take affect.
- On the left hand side we can see osticket-vm" under the connections window, right click that and choose stop. Wait for bit, then right click again and choose start.
- Minimize your IIS screen and make your way back to the osTicket Installation Files. Our next step is installing osTicket.
- To install osTicket, we must extract "osTIcket-v1.15.8", to our current folder.
- Open the osTicket folder, and copy the "upload" folder into "C:\inetpub\wwwroot" which is the root of the webserver
  ![1](https://github.com/user-attachments/assets/0b4dc356-e648-4ba8-bc9b-ef34260296f5)
- Once the folder is copied over, right click the "upload folder" and select "rename". We will rename it to "osTicket"
- Maximize IIS, and stop/start the server again!
- We will attempt to access the site by going to sites -> Default Web Site -> os Ticket -> Browse *.80 (http).
  ![1](https://github.com/user-attachments/assets/9b2d5694-8447-4b5a-b9f1-8bfa3fc94917)
- You should see the osTicket Installer page
  ![Screenshot 2024-11-18 151057](https://github.com/user-attachments/assets/a5699d31-0e3d-43c4-8c26-5ea5b464f1c8)
- Notice that there are some extensions that are not enabled, lets see if we can fix that.
- Go back to IIS -> Default -> osTicket. Double click PHP Manager, click "enable or disable extensions", and enable the following: php_imap.dll, php_intl.dll, php_opache.dll.
- The php_imap.dll, php_intl.dll, and php_opcache.dll extensions in osTicket enable email fetching via IMAP, support for multiple languages, and improved PHP performance through caching, respectively, when configured in IIS.
  ![1](https://github.com/user-attachments/assets/11e5cb05-68b1-4f69-a23f-df58ee442f28)  
- After enabling the extensions, go to your brwoser and refresh, your should notice your page has updated your recommended exentions.
  ![1](https://github.com/user-attachments/assets/ddaf8466-7085-49c5-a3db-bd578dbea2e3)
- Moving along, we must change our "C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php", to "C:\inetpub\wwwroot\osTicket\include\ost-config.php"
  ![1](https://github.com/user-attachments/assets/57f72686-18b3-4795-8b68-9f1866f22c97)
- We must now assigm permissions to "ost-config.php". We do this by right clicking "ost-config.php" -> properties -> Security -> Advanced. I will select "Disable Inheritance" to strip away all inherited permissions. This leaves us with non permissions
  ![1](https://github.com/user-attachments/assets/047bbf40-5f6d-45d3-a8c7-528eb15a8570)
- Now to set up new permissions we click Add -> Select Principal -> in the text box type everyone -> click ok -> lastly click Full Control. (I understand that it's bad practice to give everyone full permissions, I was unsure of the default account osTicket assigned to us). It should look like this...  
  ![1](https://github.com/user-attachments/assets/5ef1030f-5434-43c6-b62a-7201e0b601f1)
- Click Apply -> click Ok. This gives osTicket full control to the configuration file (in this case everyone, in a production environment it would be the admin)
- Go back to your browser, and click continue
- Fill out the osTicket Basic Install information, stopping at Database settings. We created our database on the backend, but we need to login and create another database specific for osTicket then provide the credentials.  
   ![1](https://github.com/user-attachments/assets/c1ca6d79-6656-4065-a656-42493b328b53)
- To do this we must go back to our osTicket Installation Files, and install "HeidiSQL", which is a GUI used to access MySQL (and also MariaDB, PostgreSQL, and SQL Server) databases.
  ![1](https://github.com/user-attachments/assets/60219c90-2f66-48fe-b752-0ddecbfdcabb)
- Aceept agreements, and next all the way through, install, click finish, and skip. You should now see the session manager.  
  ![1](https://github.com/user-attachments/assets/1a5f2af2-6faa-436a-8349-5f35023c66e7)
- We need to setup a connection to our database, and then setup a database for osTicket to use
- On the bottom left click new, and enter your MySQL credentials you setup prior for the user and password. Now click open. This opens up a connection to our database.  
- To create a osTicket database go to the underlined dolphin -> Create new -> Database
  ![1](https://github.com/user-attachments/assets/8a074b98-f8fb-49cf-9c5c-a371ff685d2e)
- Name the Database "osTicket", and click ok. If you look at the left column, you will see the database you just created.  
- We will now move on to the browser and continue setting up osTicket. Fill is Database Settings with teh applicable information, and click install now  
  ![1](https://github.com/user-attachments/assets/740ab422-8d25-4a13-b89b-88806537002e)  
- If everything was done correctly we have successfully setup osTicket, and all it's dependencies!  
  ![1](https://github.com/user-attachments/assets/5dd39d25-6689-4528-8b4f-fd8ae7720ce4)












