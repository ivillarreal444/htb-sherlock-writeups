# HTB Sherlock: ElectricBreeze-1 #
Your security team must always be up-to-date and aware of the threats targeting organizations in your industry. As you begin your journey as a Threat Intelligence Intern, equipped with some SOC experience, your manager has assigned you a task to test your research skills and how effectively you can leverage the MITRE ATT&CK framework. * Conduct thorough research on Volt Typhoon. * Use the MITRE ATT&CK framework to map adversary behavior and tactics into actionable insights. Impress your manager with your assessment, showcasing your passion for threat intelligence.

**[ KEY INFORMATION ](https://attack.mitre.org/groups/G1017/)**

# Task 1: Based on MITRE's sources, since when has Volt Typhoon been active? #
Using the key information above, based on MITRE's summary of the threat actor, this group has been around since at least 2021.

<img src="https://i.imgur.com/0VpXZiG.png" width="1000" height="250">

# Task 2: MITRE identifies two OS credential dumping techniques used by Volt Typhoon. One is LSASS Memory access (T1003.001). What is the Attack ID for the other technique? #
Not only has Volt Typhoon used the LSASS Memory acccess technique, but they have also utilized the NTDS technique (T1003.003), which utilizes ntds.util to create installation media for the organization's domain controller, this installation media containing the username and password hashes stored in the domain controller.

<img src="https://i.imgur.com/mZR8YPs.png" width="1000" height="100">

# Task 3: Which database is targeted by the credential dumping technique mentioned earlier? #
This one is pretty straightforward. Since the credential dumping technique is utilizing the domain controller, it is pretty obvious that the attacker is targeting the Active Directory, as the domain controller is directly tied to this database. 

# Task 4: Which registry hive is required by the threat actor to decrypt the targeted database? #
Diving deeper into the NTDS sub-technique by going to the sub-technique's [page](https://attack.mitre.org/techniques/T1003/003/), we are provided with a list of procedures that have been utilized for this specific sub-technique to be executed. One of these processes, performed by a threat actor called "Mustang Panda", utilized the SYSTEM registry hive to extract the ntds.util file needed to perform this technique.

<img src="https://i.imgur.com/OpnjLof.png" width="1000" height="75">

# Task 5: During the June 2024 campaign, an adversary was observed using a Zero-Day Exploitation targeting Versa Director. What is the name of the Software/Malware that was used? #
On [this](https://attack.mitre.org/campaigns/C0039) page, based on the summary provided, it was noted that the malware used to exploit Versa Director was VersaMem.

<img src="https://i.imgur.com/7JBt1JB.png" width="1000" height="250">

# Task 6: According to the Server Software Component, what type of malware was observed?
From Task 5, VersaMem is a web shell type malware.

# Task 7: Where did the malware store captured credentials? #
[VersaMem](https://attack.mitre.org/software/S1154/) utilizes the Data Staged:Local Data Staging (T1074.001) technique to store captured data locally in the /tmp/.tmp.data folder. 
<img src="https://i.imgur.com/YxpEoPN.png" width="1000" height="75">

# Task 8: According to MITRE’s reference, a [Lumen/Black Lotus Labs article(Taking The Crossroads: The Versa Director Zero-Day Exploitaiton.)](https://blog.lumen.com/uncovering-the-versa-director-zero-day-exploitation/), what was the filename of the first malware version scanned on VirusTotal? #

<img src="https://i.imgur.com/wDnUR58.png" width="1000" height="150">

# Task 9: What is the SHA256 hash of the file? #
<img src="https://i.imgur.com/IyHLiqW.png" width="1000" height="500">

# Task 10: According to VirusTotal, what is the file type of the malware? #
Referencing the image above, VirusTotal detects the file type as a jar file. This puts a lot of pieces together of how this file interacts with the Java Instrumentation API and Javassist.

# Task 11: What is the 'Created by' value in the file's Manifest according to VirusTotal? # 
From here we can see that the file was created by Apache Maven version 3.6.0.

<img src="https://i.imgur.com/GWID0yz.png" width="1000" height="750">

# Task 12: What is the CVE identifier associated with this malware and vulnerability? #

<img src="https://i.imgur.com/hTsSKBw.png" width="1000" height="250">

# Task 13: According to the CISA document(https://www.cisa.gov/sites/default/files/2024-03/aa24-038a_csa_prc_state_sponsored_actors_compromise_us_critical_infrastructure_3.pdf) referenced by MITRE, what is the primary strategy Volt Typhoon uses for defense evasion? #

"Living-off-the-land" attacks are when attackers utilize tools already present in the environment to carry out their attack. In this case, Volt Typhoon is utilizing this attack strategy by using zero-day vulnerabilities in the Java Instrumentation API to carry out their attack.

<img src="https://i.imgur.com/gqNXfuP.png" width="1000" height="300">

# Task 14: In the CISA document, which file name is associated with the command potentially used to analyze logon patterns by Volt Typhoon? #

<img src="https://i.imgur.com/Z9geK9j.png" width="1000" height="500">

# Conclusion #
This box taught me a lot about how research works in a typical SOC environment, which allowed me to use my Security+ as well as Blue Team CTF knowledge to understand better how to utilize the MITRE ATT&CK framework to conduct research on treat actors as well as attack techniques and how they are performed and hashed. Super easy box, but also super informative.

<img src="https://i.imgur.com/3szoTJN.png" width="500" height="500">
