# Hack The Box NetMon Educational Walkthrough

What you will learn:&#x20;

* Efficient learning practices using Hack The Box, Google search and other people
* Using ParrotOS
* Understanding the fundamentals of IP addressing&#x20;
* Understanding the fundamentals of network ports
* Using [Nmap's](https://nmap.org/) scripting engine to quickly enumerate a target
* Healthy documentation habits
* Discovering and understanding how to use CVEs
* Common configuration mistakes admins use that attackers take advantage of to own the system
* Patch management fundamentals
* Understanding the File Transfer Protocol
* Bad and Good password hygiene
* Implementing proper network segmentation techniques and firewall rules to prevent unwanted access
* Understanding web application fundamentals
* Using [Burp](https://portswigger.net/burp) to capture session cookies&#x20;
* Understanding Windows file system (NTFS) basics
* Accessing a Windows system using server message block (SMB)&#x20;

**Be on the look out for a video walkthrough that provides a more interactive guide to supplement this written walkthrough where all the learning objectives above will be fufilled.**

![](<../.gitbook/assets/image (64).png>)

![](<../.gitbook/assets/image (27).png>)

In the above image we see that this is a Windows system that is running several common services. Perhaps the most noteworthy services are FTP (port 21) and HTTP (port 80), these indicate that this Windows system is running a web server and an FTP server.&#x20;

The first service I decided to check was the web service (http port 80). This is done by entering the IP address of the target in a web browser. It is worth noting that in a real world environment, web management interfaces shouldn’t be accessible from just any device on the network. On Hack The Box’s environment this is in place on purpose for us to practice. Many applications provide options to restrict access from specific IP addresses and/or network segments. System administrators can also create rules at the network level to permit and deny access from certain segments.  Lets continue with our enumeration.&#x20;

![Accessing PRTG Admin Interface](<../.gitbook/assets/image (63).png>)

![Making note of the PRTG version installed](<../.gitbook/assets/image (33).png>)

PRTG is a network monitoring tool used in enterprise network environments and Internet Service Provider networks to monitor the status & health of network devices. It is used to monitor servers, switches, routers, access points, etc. If this box is monitoring the whole network and an attacker can breach this server, then they can own the whole network. This would especially be true if the administrators haven't been careful about running updates regularly.

This box requires further enumeration through the use of Nmap. There are several scripting modules out there for use already. &#x20;

These two articles below provide some excellent supplimentary reading if you would like to learn several NSE options built into Nmap

{% embed url="https://null-byte.wonderhowto.com/how-to/easily-detect-cves-with-nmap-scripts-0181925/" %}

{% embed url="https://securitytrails.com/blog/nmap-vulnerability-scan" %}

![Nmap default scripts show important info about the target](<../.gitbook/assets/image (56).png>)

It is possible to log in using the anonymous user account on the FTP server. This allowed us to get the user flag from the user.txt file in the Public user profile in Windows. See below for the list of commands we used.&#x20;

![Using FTP to navigate the target’s file system and download the User flag](<../.gitbook/assets/image (44).png>)

A web browser can also be used as an FTP client.

![Using the web browser as an FTP client](<../.gitbook/assets/image (66).png>)

After capturing the user.txt file from the Public directory it was time to work on getting root by exploring more about PRTG. PRTG is accessible from a web browser,  so it is safe to say that it is a [Web application](https://en.wikipedia.org/wiki/Web_application). This means the application itself is delivered using web server technologies. Like any other application, PRTG has default configuration files. Understand that system administrators often refer to the same documentation that penetration testers and malicious actors do. Good documentation makes an application easier to install, configure and manage. It can also give important details about where critical files are stored on the system. A quick Google search of: "where does PRTG keep default configuration files?" will turn up several PRTG documentation pages revealing that the configuration files are stored in the ProgramData directory. ProgramData is a hidden directory kept at the root of the C: drive in Windows. It is important to note that many different applications keep data in the ProgramData directory, including several strains of malware.

![dir -a shows us all files, including the ones that are set to hidden](<../.gitbook/assets/image (61).png>)

![Inside of the Paessler directory](<../.gitbook/assets/image (82).png>)

Using the get command allows us to download files, so I chose to download the files that seemed like they may have some useful information.&#x20;

![Using get to download files](<../.gitbook/assets/image (86).png>)

Similar to a Linux system, you must use quotes when interacting with a file or folder that has a name containing spaces. Otherwise it will not be recognized as a file that exists. FTP from the command line will pull down the files to whatever your current working directory is. The downloaded files are stored on my ParrotOS (HTB Pwnbox) home directory.

&#x20;

![My home directory with the 3 downloaded files](<../.gitbook/assets/image (59).png>)

Now that the files are on our attack system we can start searching for more important information. Keep in mind what our goal is, if we don't have a goal then we will be aimlessly poking through these files with no context and likely hit a wall. These are the pieces of information I immediately thought to look for:&#x20;

* User names&#x20;
* Passwords&#x20;
* Passphrases&#x20;
* Passkeys

We live in a search centric world and their are lots of tools at our disposal (especially in Linux distros) to speed up the search for specific data. In this case I just opened the graphical file manager (how dare I not use CLI for something... 😁 ) in ParrotOS to interact with the PRTG configuration files

![Me being a GUI baby](<../.gitbook/assets/image (67).png>)

I wasn't able to find anything in the PRTG Configuration.dat file and the other two config files provide a fun learning opportunity. Notice the warning sign on each.

![Warning sign on file](<../.gitbook/assets/image (43).png>)

Attempting to double click on this file shows that the OS does not have a default application set that knows how to read this file. This is where a text or code editor can come in handy. ParrotOS has Sublime Text installed by default so lets go with that and open the file from inside of Sublime.&#x20;

![Boom! File opens in Sublime text](<../.gitbook/assets/image (75).png>)

Now lets try the same search through Sublime Text. Keep in mind that most modern Operating Systems and applications give you the ability to search.&#x20;

![Using the search term:  password, turns up some juicy details](<../.gitbook/assets/image (72).png>)

Trying to log in to the PRTG management console with the credentials found above did not initially work so we started guessing in an educated manner. Seems that changing the year in the password worked (changed to 2019). We were then able to access PRTG management console. The admin of this system was likely just trying to make their own life easier by using this password format, this led to major security isssues. It is a good practice to set a scheduled time to change passwords on commonly used applications and accounts. It is not good to change the password to something similar just for the sake of memoriziation. This is a common mistake made by even some of the most technically savy administrators. Most will make this mistake because they want one less thing to worry about. Managing IT systems can be a hectic and time consuming job so many practices are done out of sake of convenience to reduce stress on admins. I recommend the use of a [password manager](https://www.cnet.com/how-to/best-password-manager/) to generate and store passwords. This removes the burden of needing to remember passwords, making it easier for admins to use more complex passwords that are not easy to guess manually or through automated brute force tools.

![Successfully accessed PRTG Management Interface](<../.gitbook/assets/image (42).png>)

Obtaining admin credentials for PRTG was not the golden ticket. We still needed to get to the underlying Windows system that is hosting the PRTG application. At this point there are a lot of takeaways you can  learn from this box. The three major takeaways for me at this point are:&#x20;

* Harden your default configurations. In other words don't leave default configuration settings and files.&#x20;
* A simple default configuration left on FTP allowed us to capture some files from the Public folder and a PRTG config file containing admin credentials.
* Update (patch) Operating systems and applications. An out of date application in this case leads to the full compromise of a system. It is good to develop a patch management strategy and schedule.

## Finding an exploit to get to the root of it all&#x20;

At this point we have a few different avenues we can choose to go down. We could look for a way to upload a reverse shell or we could do further enumeration on the target. In this case I chose to do further enumeration by searching for some exploits and CVEs ([Red Hats definition of CVE](https://www.redhat.com/en/topics/security/what-is-cve)) for PRTG. If you didn't already know, CVE is short for Common Vulnerabilities and Exposures. It is a list of publicly known vulnerabilities and even exploits that have been written for use. There is a command line tool that automates the process of searching for released exploits, it's called [searchsploit](https://www.exploit-db.com/searchsploit).

![SearchSploit results for PRTG Network Monitor](<../.gitbook/assets/image (30).png>)

We found two promising exploits. Notice the version number next to PRTG and compare it to the version of PRTG running on the box we are working on. This will determine which exploit we should try to use. Depending on which OS you are running you could have a copy of Exploit-DB on your distro. If none of the exploit files exist on your system you may need to manually search for the exploit through Google or on [exploit-db.com](https://www.exploit-db.com/).&#x20;

![Exploit for PRTG](<../.gitbook/assets/image (51).png>)

After downloading the exploit and studying the file we can find directions the author wrote to show users of the exploit how to use it.  This exploit creates a user account with admin privileges ,but to successfully run the exploit we must use a session cookie from a browser session we have logged in to PRTG as prtgadmin. A session cookie can be copied from the browser developer tools console or we can use Burp Suite.

![Capturing the session cookie using Burp Suite](<../.gitbook/assets/image (71).png>)

Attempting to run the exploit did not initially work. If you get an error when attempting to run this exploit it would be wise to try using a tool called dos2unix to convert the file to a format that can be used on a Linux distro.

![We needed to use dos2unix in ParrotOS to successfully execute the exploit with no errors](<../.gitbook/assets/image (80).png>)

![Command used to execute PRTG exploit](<../.gitbook/assets/image (40).png>)

![Exploit successfully creates admin account on the system](<../.gitbook/assets/image (54).png>)

As mentioned above, notice how the exploit creates a user account and password on the system for us to then use to access a share on the system. For those that don’t know, the entire C: drive on Windows is a hidden share at install. There are many ways to connect to an SMB share on Windows, in this case I just used the graphical file manager to connect using the parameters displayed in the image below:&#x20;

![Connecting to the Windows box using the graphical file manager](<../.gitbook/assets/image (45).png>)

There you have it! Full admin access to the entire file system on the Windows box. From here one can navigate to Users then to the Administrator profile with no issues and find the root.txt flag. In a real world scenario an attacker may try to establish persistence at this point, ensuring they can maintain remote access, distribute malware or even begin to pivot to other devices on the network. It is important to run updates regularly on applications & operating systems, create strong passwords and securely store any backup configuration files (especially ones containing credentials)!

Shoutouts:

* Anyone reading this for inspiring me to continue creating educational content in many formats
* [livestep](https://github.com/TheLivestep) for introducing the dos2unix tool
* Everyone who joined in on Twitch and provided good conversations&#x20;
* [Hack The Box](https://www.hackthebox.eu/) for continuing to develop an amazing platform for learning Cybersecurity

Please feel free to reach out to me if you have any thoughts, suggestions or feedback on this article. Id love to hear from you! I hope you enjoyed this educational walkthrough.&#x20;

Keep learning!



### Ways to Help & Support

You can help me continue to improve my content through feedback, words of encouragement and even if you:

[![Buy Me A Coffee](https://cdn.buymeacoffee.com/buttons/v2/default-blue.png)](https://www.buymeacoffee.com/ltnbob)
