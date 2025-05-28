# HTB Sherlock: Origin #
A major incident has recently occurred at Forela. Approximately 20 GB of data were stolen from internal s3 buckets and the attackers are now extorting Forela. During the root cause analysis, an FTP server was suspected to be the source of the attack. It was found that this server was also compromised and some data was stolen, leading to further compromises throughout the environment. You are provided with a minimal PCAP file. Your goal is to find evidence of brute force and data exfiltration.

## Task 1: What is the attacker's IP address? ##
Firstly, when examining the file, I noticed that this is not a typical .log or .wtmp file. In fact, this is a .pcap file, which is commonly known as a packet capture file. Because of this, I decided to use my Kali environment for this box, as Kali comes with Wireshark preinstalled, allowing me to utilize this application to analyze this packet capture file. 
Right off the bat, I noticed multiple failed password attempts to the server, which is a clear indicator that this was a brute force attack. Luckily enough, this packet capture gives us exactly the source of these brute force attacks, which is in fact, the attacker's IP address in clear view.

<img src="https://i.imgur.com/hAaoiD8.png" height="250" width="1000">

## Task 2: It's critical to get more knowledge about the attackers, even if it's low fidelity. Using the geolocation data of the IP address used by the attackers, what city do they belong to? ##
A simple lookup of the IP (I used an online IP locator) gives us the city origin of the IP address, which is Mumbai.

## Task 3: Which FTP application was used by the backup server? Enter the full name and version. (Format: Name Version) ##
The FTP application is listed at the first few FTP packets that were captured.

<img src="https://i.imgur.com/Y8tsTfP.png" height="500" width="2000">

## Task 4: The attacker has started a brute force attack on the server. When did this attack start? ##
To find exactly when this attack started, we need to filter the FTP packets by the attacker's IP address only. A simple display query of "ip.src = 15.206.185.207 and ftp" as well as a little bit of scrolling will take us exactly to where we need to be (NOTE: If you're using a fresh Wireshark installation for this box, you might find yourself looking at a different time than the picture. That is because Wireshark's default time format is not UTC. To change the formatting to UTC, go to "View -> Time Display Format" and select "UTC Date and Time".

<img src="https://i.imgur.com/YSBW6jR.png" height="50" width="1000">

## Task 5: What are the correct credentials that gave the attacker access? (Format username:password) ##
While we're still in this display query, we can also figure out the credentials the attacker used to gain access. Cycling through the abyss of bruteforce attempts and locating the last credentials before the successful login, we come across these credentials.

<img src="https://i.imgur.com/YSBW6jR.png" height="50" width="1000">

## Task 6: The attacker has exfiltrated files from the server. What is the FTP command used to download the remote files? ##
Since we only want ftp-data packets, let's make a display query of "ftp-packets". Now that we're here, note the command used to download 2 files from the ftp server.

<img src="https://i.imgur.com/qEsWoh5.png" height="250" width="2000">

## Task 7: Attackers were able to compromise the credentials of a backup SSH server. What is the password for this SSH server? ##
Let's inspect the files the attacker downloaded to get more information about their attack. To do this, in the Wireshark menu, let's head to "File -> Export Objects -> FTP-DATA" and save the files that Wireshark extracted. From here, I came across a pdf file that was supposed to be for scheduled maintenance, but in this pdf file, I noticed that the backup SSH server password was inside this exact file.

<img src="https://i.imgur.com/0Qu15RR.png" height="150" width="1000">

## Task 8: What is the s3 bucket URL for the data archive from 2023? ##
From the extraction we are also provided a text file that gives us the URLs that lead to the company's s3 buckets. The first URL is the one with the data archive from 2023.

<img src="https://i.imgur.com/dCT88rM.png" height="150" width="1000">

## Task 9: The scope of the incident is huge as Forela's s3 buckets were also compromised and several GB of data were stolen and leaked. It was also discovered that the attackers used social engineering to gain access to sensitive data and extort it. What is the internal email address used by the attacker in the phishing email to gain access to sensitive data stored on s3 buckets? ##
In the image above, we are provided with the alonzo's email, the exact email that was used to carry out the attacker's phishing strategy.

## Conclusion ##
This box gave a pretty clear introduction as to how to use Wireshark to analyze network packet captures, something that I have noticed that is starting to become very useful in the SOC/DFIR environment. From this box alone I am beginning to realize how powerful of a tool Wireshark can be, and I'm super excited to learn more about this tool in the future. 

<img src="https://i.imgur.com/zvrhVJi.png" height="500" width="500">
