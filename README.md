# shehacks.github.io
My cybersecurity journey

LAB CHALLENGES
WEB APPLICATION BASED ATTACKS using GVM Vulnerability Scanner
GVM is part of the Open-Source Vulnerability Management suite of products produced by Greenbone Networks GmbH. The GVM scanner is one of the most widely used open-source vulnerability scanners. Unlike Nmap, GVM uses a graphical user interface to initiate scans and report vulnerability scan results.
PART 1: Scan a Host for Vulnerabilities
Start GVM services
Start the GVM scanner using the sudo gvm-start command. You can also access the gvm-start script using the Applications menu on the Kali desktop
┌──(kali㉿Kali)-[~]
└─$ sudo gvm-start
Note: You may receive the message “GVM services are already running.” If the browser does not automatically open, start your browser manually and navigate to https://127.0.0.1:9392. The Greenbone Security Assistant login screen will appear in the browser.
In the Greenbone Security Assistant login box, enter admin as the username and kali as the password.
Username: admin
Password: kali
Step 2: Scan a host.
You will scan the Metasploitable vulnerable host using the GVM scanner. 
The GVM Scanner application GUI should open in the browser. Select Scans -> Tasks from the menu bar. Select the Task Wizard icon. Choose Advanced Task Wizard from the dropdown menu.
In the Advanced Task Wizard window, enter Metasploitable as the scan name. In the Target Host(s) field, enter the IP address of Metasploitable, 172.17.0.2. Leave the rest of the settings unchanged and click Create to create the task and start the scan.
The Task window indicates the task is running. At the bottom of the window, the task Metasploitable is listed, and the status bar shows the percent complete. Wait until the status shows Done (100% complete).
Click the number 1 under the Reports column in the Metasploitable row, next to the status indicator. The report list opens with an entry for the current day and time and the task named Metasploitable.
Click the number 1 under the Reports column in the Metasploitable row, next to the status indicator.
Open the report by clicking the date and time link under the Date column. Click the Results tab. The vulnerabilities found are listed in order of severity.
Click the Results tab. The vulnerabilities found are listed in order of severity.
Step 3: Interpret the scan results.
Click the The rexec service is running vulnerability listed in the Results tab. GVM provides a summary of the finding and additional details. The Insight section explains a little about the vulnerability and the Solution section gives mitigation suggestions.
Click the back arrow in the browser to return to the report screen. The rexec services typically run on TCP ports 512, 513, or 514. For this it's 512
Part 2: Exploit a Vulnerability Found by GVM
Step 1: Perform reconnaissance against the target.
Administrators and other users often reuse passwords, use weak passwords, or fail to change the default credentials for a service. From a previous lab, we learned about vulnerabilities in SMB. We will use Nmap to see if we can learn anything from SMB about accounts that we might be able to use with rexec.
Use the Nmap script smb-brute to find users and to attempt to brute force passwords.
┌──(kali㉿Kali)-[~]
└─$ sudo nmap -sV -p 445 -script smb-brute 172.17.0.2
Locate the Host script results section in the command output. Username and password combinations that were uncovered with the Nmap scrip
Step 2: Perform the rexec exploit.
To access the Metasploitable target to exploit the rexec vulnerability, you will need a remote shell client. Use apt-get to install a remote shell (RSH) client on the Kali Linux VM.
┌──(kali㉿Kali)-[~]
└─$ sudo apt-get install rsh-client
Attempt to log in to the Metasploitable target with the username msfadmin using RSH. The syntax for the rsh command is rsh -l [username] [target IP or hostname]
┌──(kali㉿Kali)-[~]
└─$ rsh -l msfadmin 172.17.0.2
(ERROR MESSAGE!!!!)
