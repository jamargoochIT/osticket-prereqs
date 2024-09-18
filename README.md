<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Item 1
- Item 2
- Item 3
- Item 4
- Item 5

<h2>Installation Steps</h2>

<p>
Now that we’ve logged into our Virtual Machine, we’re going to enable and install IIS with CGI in Windows. 
IIS is a webserver that will run on the virtual machine. This webserver is going to be running osTicket.

CGI is a dependency that osTicket needs for the webserver.


Type control panel in the Windows Search Bar and open the app. Click on to programs and features.
 
 

- On the left side, click Turn Windows features on or off.
 

- Click the box next to Internet Information Services, then click plus button to the left of the box we checked.
 

- World Wide Web Services -> Application Development Services -> click the box next to CGI.
 

- Click ok and wait for the changes to be applied.

After the webserver is installed, we'll need to download the following:

Image 4  



Fist up, PHPManagerForIIS_V1.5.0.msi.
PHP is a backend webserver language that osTicket runs on. Now we’ll click on the exe to install it.
Image 5 


After that's done, we'll need to install rewrite_amd64_en-US.msi, which changes complicated URLs into simpler ones, enabling osTicket’s URLs to look simpler and easier to manage.
Let’s click on the exe to install it.
Image 6 


Now let’s create a folder in the C drive named PHP.

Alright, now we’re going to unzip the PHP files that osTicket is going to use onto the C drive.
Unzip php-7.3.8-nts-Win32-VC15-x86.zip to the PHP folder you just created on the C drive.
Image 7 


After that’s finished, we’re going to install VC_redist.x86.exe. Which installs Visual C++ redistributable, giving osTicket the tools to operate properly. 

Let’s click on the exe to get the installation started.
Image 8 


MySQL 5.5.62-win32 is going to install a MySQL Server which is a database that osTicket is going to store all of our data in, such as user accounts, ticketing information, etc.

Let’s click on the exe to get started.



Image 9 
When this window opens up, select Typical.

Image 10 


Launch the configuration wizard.

Image 11 


Select standard configuration.

Image 12 


Select next.

Image 13 


Here we’ll need to create a password, for the Root user, for simplicity, I'll use boot for my password.
You’ll want to use something more secure. Remember the password you make as we’ll be using it when we get to HeidiSQL.



Image 14 


Now, click execute.

Open up IIS as an administrator.

Image 15 

Now, we’re going to make the webserver aware of PHP being installed on the VM and tell it where it is.

Click on PHP Manager -> Register new PHP version. 

Image 16 


Start and stop the server in IIS using the buttons on the right side.

Image 17 


Now we're off to install osTicket. First, unzip osTicket-v1.15.8.zip. Copy the folder upload into the C drive folder wwwroot.
Path C:\inetpub/wwwroot.

Image 18 


After we’ve copied the upload folder to the destination above, rename the upload folder to osTicket. When you rename the upload folder to osTicket, it needs to be spelled exactly like this: osTicket.


Image 19 


Once again, run IIS as an admin. Restart the server by right-clicking on virtual-ticket on the left side and selecting stop, then, once the server has stopped, right-click it again and select start. 
Now On the left side, we’ll go down this path, virtual-ticket -> Sites -> Default Web Site -> osTicket.

Image 20 


Here is where we’ll attempt to load the osTicket site. 
On the far-right side, click on Browse .80

Image 21 


And now the osTicket site should open in our browser. 

Image 22 


Now we’ll go back into IIS and go down the path: virtual-ticket -> Sites -> Default Web Site -> osTicket. Then double-click PHP Manager.

Image 23 


Click on Enable or disable an extension.

Image 24 


Then enable (through right-clicking) the following PHP extensions:
- php_imap.dll
- php_intl.dll
- php_opcache.dll

Image 25 
These extensions help osTicket handle emails, support multiple languages, and run faster.


When we’ve finished enabling the PHP extensions, we’ll refresh osTIcket in our browser.

Image 26 


And it should change to the following

Image 27 


Next up, we'll want to rename the file, ost-sampleconfig.php to ost-config.php. We’re renaming the file because the ost-sampleconfig has sample settings, and renaming it allows osTicekt to use the actual configuration file.

The path to this file is the following: C: -> inetpub -> wwwroot -> osTicket -> include -> ost-sampleconfig.php

Image 28 


Now we’re going to make sure osTicket has access to this file. Right-click the ost-config.php file. Go to properties. Go to the security tab and click on advanced.

Image 29 


Click Disable inheritance.

Image 30  


Select, Remove all inherited permissions from this object.

Image 31 


Then click Add, and the select a principal. 

Image 32 


When you assign permissions, you will want to give permissions to specific users, such as Admins. But since I don’t have a network of users, I’m just going to type Everyone.
After we type in the permission, we can click OK.
Image 33 


Now click Full control and then click OK.

Image 34 


Then click apply and then OK and OK again.

Image 35 


Now we’ll go back to osTicket in our browser press continue.

Image 36 


Now we’ll fill out the required fields that are highlighted in the image.

Image 37 


For the final time, back to the osTicket-Installation-Files folder.
We need to log into the backend database we created earlier (My SQL) and create another database specific to osTicket then provide the credentials for it.
To do that we need to install HeidiSQL.
HeidiSQL is an application that allows us to make a connection to and configure our database.


Image 38 


We’ll click next all the way through until we get the option to install. Now we’ll install the client.

When the installation finishes, launch HeidiSQL.

Image 39 


Click Skip.

Image 40 


Now we’ll make a connection to our database and setup a database for osTicket to use and put that information into the required fields to finish installing osTicket.
Click New.

Image 41 


The user is automatically filled out as root because we set up our SQL server earlier and the Root user a password. Now we’ll type in the password we created when we setup the SQL server to connect HeidiSQL to it.

Image 42 


In the right menu, right click and select create new, and then select database. Name the database osTicket.

Image 43 


We're almost at the finish line.

Back in the osTicket in our browser, we’ll finish filling out the bottom fields by entering the name and password of the database we just created in Heidi into the SQL database field: 

- MySQL Database: osTicket
- MySQL Username: boot
- MySQL Password: boot

Image 44 


Now, finally, click Install Now!

Image 45 



This is the screen we get next: 

Image 46  


Now click on the link below: Your Staff Control Panel.

It should bring us to:

Image 47 


Now all you need to do is log in with the credentials we made in the Database Setting to finish installing osTIcket: 
 





And that’s it, we’ve set up osTicket.

</p>
<br />
