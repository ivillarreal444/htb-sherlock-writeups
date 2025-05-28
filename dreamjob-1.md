# HTB Sherlock: Dream Job-1 #
You are a junior threat intelligence analyst at a Cybersecurity firm. You have been tasked with investigating a Cyber espionage campaign known as Operation Dream Job. The goal is to gather crucial information about this operation.

**[Key Information](https://attack.mitre.org/campaigns/C0022/)**

## Task 1: Who conducted Operation Dream Job? ##
Using the key information above, we can see that Operation Dream Job was likely conducted by the Lazarus Group. 

<img src="https://i.imgur.com/8I5JskN.png" width="1000" height="250">

## Task 2: When was this operation first observed? ##
Using the information on the right of the summary of the operation, we can see that this operation was first observed in September 2019.

<img src="https://i.imgur.com/off0le7.png" width="450" height="250">

## Task 3: There are 2 campaigns associated with Operation Dream Job. One is Operation North Star, what is the other? ##
Below the summary we are provided a list of associated campaigns that are associated with Operation Dream Job, the first being Operation North Star, and the second being Operation Interception.

<img src="https://i.imgur.com/Jog4FHF.png" width="1000" height="175">

## Task 4: During Operation Dream Job, there were the two system binaries used for proxy execution. One was Regsvr32, what was the other? ##
This attack technique is known as System Binary Proxy Execution, or T1218. Searching this on the page we come across two sub-techniques: Regsvr32 (T1218.010) abd Rundll32 (T1218.011).

<img src="https://i.imgur.com/nVpDMqH.png" width="1000" height="100">

## Task 5: What lateral movement technique did the adversary use? ##
By comparing the [list of lateral movement techniques](https://attack.mitre.org/tactics/TA0008/) to the list of techniques that Lazarus Group used during Operation Dream Job, we notice that Internal Spearphishing (T1534) is the lateral movement technique that Lazarus Group used.

<img src="https://i.imgur.com/WJQJuTz.png" width="1000" height="50">

## Task 6: What is the technique ID for the previous answer? ##
From Task 5: "we notice that Internal Spearphishing (**T1534**) is the lateral movement technique that Lazarus Group used."

## Task 7: What Remote Access Trojan did the Lazarus Group use in Operation Dream Job? ##
At the bottom of the main page, we can see a list of software that Lazarus group used during Operation Dream Job. Clicking on the first one, DRATzaurus, we are forwarded to the page of the software, with the software's summary basically confirming that this software is a Remote Access Trojan. 

<img src="https://i.imgur.com/MwhMPRd.png" width="1000" height="200">

## Task 8: What technique did the malware use for execution? ##
This one took me a while to figure out, but by looking at what Task 7 was asking, I tried looking for anything related to sandbox detection evasion, and the only one that seemed to stand out for me was the Native API technique, which ended up being the right answer to this task.
<img src="https://i.imgur.com/wo7xkhe.png" width="1000" height="50">

## Task 9: What technique did the malware use to avoid detection in a sandbox? ##
From here, we'll need to find a subtechnique the malware used that belongs to the Virtualization/Sandbox Evasion (T1497) technique. Scrolling to the bottom of the malware's "Techniques Used" column, we can see that the malware used one subtechnique that fits our criteria.

<img src="https://i.imgur.com/IAonRau.png" width="1000" height="50">

## Task 10: To answer the remaining questions, utilize VirusTotal and refer to the IOCs.txt file. What is the name associated with the first hash provided in the IOC file? ##
This one is pretty straightforward. Just plug the first hash into VirusTotal and the file name will be shown immediately.

<img src="https://i.imgur.com/qZPGCBs.png" width="1000" height="150">

## Task 11: When was the file associated with the second hash in the IOC first created? ##
Plugging the second hash into VirusTotal, we'll need to find the creation time for the file. Heading into the details section of the VirusTotal page, we can find the creation date in the "Hiatory" section.

<img src="https://i.imgur.com/ALekCrc.png" width="1000" height="150">

## Task 12: What is the name of the parent execution file associated with the second hash in the IOC? ##
This one also took me a little bit of time, but I found that in the "Relations" page of the site, there exists an "Execution parents" column, which contained the name of the parent execution file we need.

<img src="https://i.imgur.com/JFJLj3g.png" width="1000" height="100">

## Task 13: Examine the third hash provided. What is the file name likely used in the campaign that aligns with the adversary's known tactics? ##
Plugging the third hash into VirusTotal, we can see in the "Names" column in the "Details" section a file that aligns with the adversary's known tactics.

<img src="https://i.imgur.com/sXJAdt3.png" width="750" height="350">

## Task 14: Which URL was contacted on 2022-08-03 by the file associated with the third hash in the IOC file? ##
This one took me a while to find, mainly because the comment column in the "Community" section does not display actual dates of the comments anymore, so after doing a little searching around the comments, I found one that contains a URL associated with an IOC, and this link ended up being the answer to the task. 

<img src="https://i.imgur.com/m3UoyW6.png" width="1000" height="350">

## Conclusion ##
This box gave me an introduction to VirusTotal and how it can be utilized to get lots of information about an attack. VirusTotal is very useful in the industry as it provides a lot of useful information on malware that can help determine what exactly attackers are doing, and what exactly the attackers are going after.

<img src="https://i.imgur.com/bhH6s4H.png" width="750" height="750">
