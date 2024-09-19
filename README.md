<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the help desk ticketing system osTicket.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

![image](https://github.com/user-attachments/assets/1610e54b-03b5-4df2-ad66-38a6b3051af7)<br><br><br><br><br>



<h2>Installation Steps</h2>


Now, we’re going to go through the installation process for osTicket. 
After we log into our Virtual Machine, we’re going to enable and install Internet Information Services (IIS) with Common Gateway Interface (CGI) in Windows. 

IIS (Internet Information Services) is a web server that hosts websites and web applications. This webserver is going to run osTicket.
CGI (Common Gateway Interface) is a standard way for a web server to communicate with scripts that can create web pages.
CGI handles submitting tickets, saving tickets, sending emails, and user requested retrieving information.


Type control panel in the Windows Search Bar and open the app. Click on to programs and features.


 
![image](https://github.com/user-attachments/assets/a6afd495-de25-43ea-aec7-98ab4349db97)
![image](https://github.com/user-attachments/assets/00d8e013-4fde-47dc-9f50-0de4e8c02697)<br><br><br><br>



On the left side, click Turn Windows features on or off.


![image](https://github.com/user-attachments/assets/b4ff03b8-12e9-423c-8798-3ea3aefee9c6)<br><br><br><br>


Click the box next to Internet Information Services, then click the plus button to the left of the box we checked.

![image](https://github.com/user-attachments/assets/aaa1f002-85a2-4e44-ac1e-eaf270750ad0)<br><br><br><br>


World Wide Web Services -> Application Development Services -> click the box next to CGI.

![image](https://github.com/user-attachments/assets/9428c221-0c3b-4b50-ac0d-a2ffce3ad385)<br><br><br><br>

 
Click ok and wait for the changes to be applied.

After the webserver is installed, we'll need to download the following:

![image](https://github.com/user-attachments/assets/8adb9afa-e9f9-4ef2-aea2-685f181f8009)<br><br><br><br>




Fist up, PHPManagerForIIS_V1.5.0.msi.
PHP is a backend webserver language that osTicket runs on. 
Now we’ll click on the exe to install it.

![image](https://github.com/user-attachments/assets/9bd5fd29-17ea-431a-b071-1bf7f9bcf77b)<br><br><br><br>



After that's done, we'll need to install rewrite_amd64_en-US.msi, which changes complicated URLs into simpler ones, enabling osTicket’s URLs to look simpler and become easier to manage.
Let’s click on the exe to install it.

![image](https://github.com/user-attachments/assets/65ac1d42-62cc-49c6-a77a-abdfa77fa147)<br><br><br><br>



Now let’s create a folder in the C drive named PHP.

On the C drive we’re going to unzip the PHP files that osTicket is going to use.

Unzip php-7.3.8-nts-Win32-VC15-x86.zip to the PHP folder you just created on the C drive.

![image](https://github.com/user-attachments/assets/393dc89e-0314-42a3-83d6-0000d2adf737)<br><br><br><br>



After that’s finished, we’re going to install VC_redist.x86.exe. Which installs Visual C++ redistributable, which is like a toolbox that osTicket needs to operate correctly. Installing it ensures that all the parts osTicket relies on are available on our virtual machine.

Let’s click on the exe to get the installation started.
Now click on the box next to I agree and click Install. 

![image](https://github.com/user-attachments/assets/f08b09a0-e44d-48fe-a5d5-2f20e93c5e54)<br><br><br><br>


MySQL 5.5.62-win32 is going to install a MySQL Server which is a database that osTicket is going to store all of our data in, such as user accounts, ticketing information, etc.

Let’s click on the exe to get started.
When this window opens up, select Typical.



![image](https://github.com/user-attachments/assets/cb1e9bd8-a3c8-4f02-a784-353036fa279a)<br><br><br><br>




Launch the configuration wizard.



![image](https://github.com/user-attachments/assets/3ab555b2-6966-4350-aff3-d4bc1afbb15c)<br><br><br><br>



Select standard configuration.



![image](https://github.com/user-attachments/assets/e858e5df-0b83-4730-90fd-70b265dc3a26)<br><br><br><br>



Select next.




![image](https://github.com/user-attachments/assets/338e8360-e498-40d4-8460-ecbbefaf4081)<br><br><br><br>



Here we’ll need to create a password, for the Root user, for simplicity, I'll use boot for my password.
You’ll want to use something more secure. Remember the password you make as we’ll be using it when we get to HeidiSQL.



![image](https://github.com/user-attachments/assets/1d624a1b-60cb-462d-b788-020af9d11e05)<br><br><br><br>


Now, click execute.

![image](https://github.com/user-attachments/assets/a6594806-cc0d-4892-8e30-d1b858420d97)<br><br><br><br>



Now, we’re going to make the webserver aware that PHP has been installed on the VM and tell it where it is.
Open up IIS as an administrator.
Click on PHP Manager -> Register new PHP version. Follow this path -> C drive -> PHP -> PHP-cgi.exe.
![image](https://github.com/user-attachments/assets/60485847-bd2b-4872-b867-b15956d35d5f)
![image](https://github.com/user-attachments/assets/07d419df-7c1c-4572-bcd2-042e6f2a2d88)<br><br><br><br>



Start and stop the server in IIS using the buttons on the right side.

![image](https://github.com/user-attachments/assets/4d00938d-a892-40e8-ae96-b00d4b853f47)<br><br><br><br>



Now we're off to install osTicket. First, unzip osTicket-v1.15.8.zip. Copy the folder upload into the C drive folder wwwroot.
Path C:\inetpub -> wwwroot.

![image](https://github.com/user-attachments/assets/1e3e6c63-bb61-4c65-aaea-e86b5d2972d9)<br><br><br><br>



After we’ve copied the upload folder to the destination above, rename the upload folder to osTicket. When you rename the upload folder to osTicket, it needs to be spelled exactly like this: osTicket.


![image](https://github.com/user-attachments/assets/2ade9cc8-f8ec-47a8-a45e-b1a117b67c18)<br><br><br><br>



Once again, run IIS as an admin. Stop and then start the server by right-clicking on virtual-ticket on the left side and selecting stop, then, once the server has stopped, right-click it again and select start. 
Now On the left side, we’ll go down this path, virtual-ticket -> Sites -> Default Web Site -> osTicket.


![image](https://github.com/user-attachments/assets/ff60b0c2-781c-4964-a1b2-ef05672dfa43)<br><br><br><br>



Here is where we’ll attempt to load the osTicket site. 
On the far-right side, click on Browse .80


![image](https://github.com/user-attachments/assets/c49507a5-e95d-43d9-83b2-1e1ba7633977)<br><br><br><br>



And now the osTicket should open in our browser.



![image](https://github.com/user-attachments/assets/7cf27682-feb6-4d4a-9cdd-269d86abab30)<br><br><br><br>



Now we’ll go back into IIS and go down the path: virtual-ticket -> Sites -> Default Web Site -> osTicket. Then double-click PHP Manager.


![23](https://github.com/user-attachments/assets/a551c20c-7cba-4808-8835-3a71d1c18b34)<br><br><br><br>




Click on Enable or disable an extension.


![24](https://github.com/user-attachments/assets/3fd483ea-16ee-4696-824e-c14e8cb0884a)<br><br><br><br>



Then enable (through right-clicking) the following PHP extensions:
- php_imap.dll
- php_intl.dll
- php_opcache.dll
They'll be in the greyed out disabled section.

![image](https://github.com/user-attachments/assets/c6e5c638-8044-48be-a76e-85462cc204f0)<br><br><br><br>


These extensions help osTicket handle emails, support multiple languages, and run faster.


When we’ve finished enabling the PHP extensions, we’ll refresh osTIcket in our browser.


![image](https://github.com/user-attachments/assets/9fc9b737-0800-438a-8881-7aafd9fc2173)<br><br><br><br>



And it should change to the following:


![image](https://github.com/user-attachments/assets/14fffd29-4a6d-4bc8-a728-a968acca12bd)<br><br><br><br>



Next up, we'll want to rename the file, ost-sampleconfig.php to ost-config.php. We’re renaming the file because the ost-sampleconfig has sample settings, and renaming it allows osTicekt to use the actual configuration file.

The path to this file is the following: C: -> inetpub -> wwwroot -> osTicket -> include -> ost-sampleconfig.php


![image](https://github.com/user-attachments/assets/3f45bcc6-2082-4188-9339-995e4eb2e328)<br><br><br><br>



Now we’re going to make sure osTicket has access to this file. Right-click the ost-config.php file. Go to properties. Go to the security tab and click on advanced.


![29](https://github.com/user-attachments/assets/5c9c71f2-ac27-4d4d-9686-22d129f6716f)<br><br><br><br>




Click Disable inheritance.


![image](https://github.com/user-attachments/assets/a392d087-8773-4959-b308-b6e650c624c6)<br><br><br><br>



Select, Remove all inherited permissions from this object.


![image](https://github.com/user-attachments/assets/4d7b3038-44d2-4c99-bd25-19bd0fbd18dc)<br><br><br><br>



Then click Add, and then click Select a principal. 


![32](https://github.com/user-attachments/assets/24df46bb-0881-4426-92a6-1048b180db7e)<br><br><br><br>




When you assign permissions, you will want to give permissions to specific users, such as Admins. But since I don’t have a network of users, I’m just going to type Everyone.
After we type in the permission, we can click OK.


![33](https://github.com/user-attachments/assets/4a9f6e26-bcc3-47cf-b0f1-3298929616db)<br><br><br><br>




Now click Full control and then click OK.


![image](https://github.com/user-attachments/assets/eefb5bad-e967-4628-91a8-77e71b143eea)<br><br><br><br>



Then click apply and then OK and OK again.


![image](https://github.com/user-attachments/assets/916760ef-3002-4eb5-bb87-632c68864bd1)<br><br><br><br>



Now we’ll go back to osTicket in our browser and press continue.


![image](https://github.com/user-attachments/assets/79c48ad0-1b78-4016-9f41-a3e43013c102)<br><br><br><br>



Now we’ll fill out the required fields that are highlighted in the image.


![image](https://github.com/user-attachments/assets/b39978ae-d627-438c-9010-faead0ecc0eb)<br><br><br><br>



For the final time, let's go back to the osTicket-Installation-Files folder.
We need to log into the backend database we created earlier (My SQL) and create another database specific to osTicket then provide the credentials for it.

To do that we need to install HeidiSQL.

HeidiSQL is an application that allows us to make a connection to and configure our database.


![image](https://github.com/user-attachments/assets/925e0c87-ebf3-4c8e-8fbe-e8658bb8b07e)<br><br><br><br>



We want to keep all the default settings, so we’ll click next all the way through until we get the option to install. Now we’ll install the client.


When the installation finishes, launch HeidiSQL.


![image](https://github.com/user-attachments/assets/32771cdb-991d-4a37-bf16-87da9ae295af)<br><br><br><br>



Click Skip.


![image](https://github.com/user-attachments/assets/d029dafb-c26d-4a4b-acf2-320996eba52d)<br><br><br><br>



Now we’ll make a connection to our database and setup a database for osTicket to use and put that information into the required fields to finish installing osTicket.

Click New.


![image](https://github.com/user-attachments/assets/43e2bffb-b2eb-413e-88e0-2a4916c1ae1b)<br><br><br><br>



The user is automatically filled out as root because we set up our SQL server earlier along with the Root user password. 

Here is when we created the password.

![image](https://github.com/user-attachments/assets/372ef859-01a0-4764-abf4-13783cb2e287)<br><br><br><br>


Now we’ll type in the password we created when we setup the SQL server to connect HeidiSQL to it.


![image](https://github.com/user-attachments/assets/e4133bd1-b3b0-4a10-a75f-a42606b97cc7)<br><br><br><br>


In the right menu, right click and select create new, and then select database. Name the database osTicket.


![image](https://github.com/user-attachments/assets/2a191a80-bcc2-42e1-a765-7e056a2d880e)<br><br><br><br>



We're almost at the finish line.

Back to osTicket in our browser, we’ll finish filling out the bottom fields by entering the name and password of the database we just created in Heidi into the SQL database fields: 

- MySQL Database: osTicket
- MySQL Username: boot
- MySQL Password: boot


![image](https://github.com/user-attachments/assets/82c9a2c0-5331-47c9-866e-757d6e7cf7c0)<br><br><br><br>



Now, finally, click Install Now!


![image](https://github.com/user-attachments/assets/6b2a5c45-8ba6-4ddf-90b7-0916b4edb39a)<br><br><br><br>



This is the screen we should get next: 


![image](https://github.com/user-attachments/assets/c369e0db-e4f3-4b62-b704-0197d8d7962f)<br><br><br><br>
 


Now click on the link below: Your Staff Control Panel.

It should bring us to:


![image](https://github.com/user-attachments/assets/3fa4aa4e-c973-4258-8750-99f2c662adfc)<br><br><br><br>



Now all you need to do is log in with the credentials we made in the Admin User section of the osTicket Basic Installation page.
 

![image](https://github.com/user-attachments/assets/97767470-bbc1-4311-a628-bc855f875339)<br><br><br><br>




And that’s it, we’ve set up osTicket.


</p>
<br />

