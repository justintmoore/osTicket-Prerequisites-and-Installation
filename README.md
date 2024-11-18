
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
- Review and Create VM
- 








