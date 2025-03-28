# Sherlock - Origins

* **Category:** DFIR
* **Difficulty:** Very Easy

### Description of Scenario
A major incident has recently occurred at Forela. Approximately 20 GB of data were stolen from internal s3 buckets and the attackers are now extorting Forela. During the root cause analysis, an FTP server was suspected to be the source of the attack. It was found that this server was also compromised and some data was stolen, leading to further compromises throughout the environment. You are provided with a minimal PCAP file. Your goal is to find evidence of brute force and data exfiltration. The file can be extracted [here](https://challenges-cdn.hackthebox.com/sherlocks/very-easy/Origins.zip?u=64669&p=mp&e=1743146657&t=1743139457&h=2985ed8885224aab94a7fb00d463481a7cf01bc03825b6a74fa7f85d18fc6b77) and the password is *hacktheblue*.

### Tasks to Execute

1. **What is the attacker's IP address?**

Let's do some brief analysis of the pcap file we have received for further investigation. For this, we are going to use `wireshark` which you can download it [here](https://www.wireshark.org/download.html). 

Opening the file named `ftp.pcap` we can review the following: it has a total of 547 packets therefore it will not be that complicated to find the information we need to solve this Sherlock. In addition, I suggest you also use the `tshark` utility just to keep sharpening those packet capture skills via the terminal. 

Before applying any kind of filtering, let's do something easier. Head to Statistics -> Conversations and checking both the IPv4 and TCP tabs, we can analyse the following:

![](/Writeups/HackTheBox/Sherlocks/Origins/Figure1.jpg)

* The IP address ***15.206.185.207*** (Now *AttackerIP*) is sending 444 packets to the server, which IP address is ***172.31.45.144*** (*ServerIP*).
* AttackerIP is sending 70 packets to ServerIP via port 21, which is referred to the FTP service. 

In conclusion, the IP address we are looking for is **15.206.185.207** and from the analysis at the TCP tab, we can conclude the brute-force attack was directed to the FTP server. Just for some brief remember, A brute-force attack is a trial-and-error method used to gain unauthorized access to a system, account, or encrypted data. In this attack, an attacker systematically tries all possible combinations of passwords, keys, or credentials until the correct one is found.

For example, in the context of an FTP server, an attacker might repeatedly attempt to log in by guessing different username-password combinations. Brute-force attacks can be time-consuming and resource-intensive, but they can succeed if weak or commonly used passwords are in place.

To mitigate such attacks, techniques like rate limiting, account lockouts, and strong password policies are often implemented.

2. **It's critical to get more knowledge about the attackers, even if it's low fidelity. Using the geolocation data of the IP address used by the attackers, what city do they belong to?**

This is quite straight forward. We can use any geoIP online tool like `ipinfo` for instance. For this case I opted for `ip-lookup` from [iplocation](https://www.iplocation.net/ip-lookup). This is a very powerful tool because it also extracts data from common locators such as `ipinfo, DB-IP, IP2Location, etc`. Analysing the data from this tool, we can appreciate the IP address belongs to India, more specifically to **Mumbai**, our second answer.

![](/Writeups/HackTheBox/Sherlocks/Origins/Figure2.jpg)

3. **Which FTP application was used by the backup server? Enter the full name and version. (Format: Name Version)**

#### What is FTP?

FTP, or File Transfer Protocol, is a standard network protocol used to transfer files between a client and a server over a computer network. It operates on a client-server model, where the client initiates the connection to the server to upload or download files. FTP is widely used for transferring large files, managing website content, and sharing data between systems.

FTP typically uses two ports for communication:
- **Port 21**: This is the control port, used to establish the connection and send commands between the client and server.
- **Port 20**: This is the data port, used for transferring the actual files (in active mode).

#### Common FTP Response Messages

When interacting with an FTP server, the server responds to client commands with numeric codes and messages. Some of the most common response messages include:

- **220**: Service ready for a new user (indicates the server is ready to accept a connection).
- **331**: User name okay, need password (indicates the username is accepted, and the server is waiting for the password).
- **230**: User logged in, proceed (indicates successful authentication).
- **530**: Not logged in (indicates authentication failure).
- **550**: Requested action not taken (indicates an error, such as a file not found or permission denied).

Understanding these codes is crucial for diagnosing issues and analyzing FTP traffic during investigations.

For this exercise, we can use the filter `ftp` which only focuses on showing FTP packets. In the Info column, you will notice all the activity over the FTP server. When you get a 220 response, it normally shows you the name of the service/daemon including the version. For this exercise it is **vsFTPd 3.0.5**.

![](/Writeups/HackTheBox/Sherlocks/Origins/Figure3.jpg)

4. **The attacker has started a brute force attack on the server. When did this attack start?**

#### What is a Brute Force Attack?

A brute force attack is a method used by attackers to gain unauthorized access to a system, account, or encrypted data by systematically trying all possible combinations of passwords, keys, or credentials until the correct one is found. This type of attack relies on computational power and persistence rather than exploiting vulnerabilities in the system.

In logs from a server, reports of a SIEM and a pcap like this, we can easily conclude that a brute force attack is performed by multiple login attempts from the same IP address. We can even conclude the attacker used the tool `Hydra` for this purpose. Let's use the filter `ip.src == 15.206.185.207 && ftp` to get all the FTP traffic and when we have multiple FTP requests at the same time, that is the attack pattern we are looking for. In addition, we must change the date format. Let's go to *View -> Time Display Format -> UTC Date and Time of Day*. With all those small tweaks we can check the first packet of the FTP conversation, and extract the accurate date which is **2024-05-03 04:12:54**.

5. **What are the correct credentials that gave the attacker access? (Format username:password)**

Using the `ftp` filter, let's look for a packet. When a successful login is done you receive a 230 response from the FTP server. For this, let's go to Go -> Go to Packet and you will receive a text box below the filter. Select `string` and sue the `successful` key word. We can follow that TCP stream and we can see that the username and password is **forela-ftp:ftprocks69$**

![](/Writeups/HackTheBox/Sherlocks/Origins/Figure4.jpg)


6. **The attacker has exfiltrated files from the server. What is the FTP command used to download the remote files?**

Normally you use the GET command in FTP to download a file but let's review a little what is happening. After we found the successful login as forela-ftp, we can follow all the TCP Stream and we can see some interesting information:

* The attacker gained some information about the compromised server throught the SYST command and its features with the FEAT command. 
* The attacker entered in extended passive mode with the EPSV command. This is normally used in systems behind a firewall.
* Switched to binary mode for faster transfer rate and also preservation of integrity of downloaded/uploaded files to the FTP server.
* Downloaded a file named Maintenance-Notice.pdf with the **RETR** command which stands for RETRIEVE. That is our answer.

7. **Attackers were able to compromise the credentials of a backup SSH server. What is the password for this SSH server?**

Wireshark is so powerful that you can even download files from a traffic packet capture. Let's go to *File -> Export Objects -> FTP-DATA* and select both files involved. This is because these files would be useful for the rest of the exercise. The PDF file is a notification about a maintenance but here is some information. 

At the *Contingency Plan* section there is an indication for the access to the backup SSH server mentioning the password **\**B@ckup2024!**\**.

8. **What is the s3 bucket URL for the data archive from 2023?**

Opening the text file we see the answer which is: **https<nolink>://2023-coldstorage.s3.amazonaws.com**

9.  **The scope of the incident is huge as Forela's s3 buckets were also compromised and several GB of data were stolen and leaked. It was also discovered that the attackers used social engineering to gain access to sensitive data and extort it. What is the internal email address used by the attacker in the phishing email to gain access to sensitive data stored on s3 buckets?**

Getting back to the text file at the end of the document we have the email address which is **archivebackups<nolink>@forela.co.uk**.

I hope you enjoyed and also learn. I found fun to do some investigation, explore some tools in this case WireShark and leveraged some features that I find it very useful. Happy hunting and pwning.

Greetings,

DrJpp