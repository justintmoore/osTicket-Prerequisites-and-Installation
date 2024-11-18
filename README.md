
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
- <a href="http://localhost/osticket/scp/login.php">http://localhost/osticket/scp/login.php</a> is the URL we can login as Admins and End Users can login with <a href="http://localhost/osticket">http://localhost/osticket</a>











