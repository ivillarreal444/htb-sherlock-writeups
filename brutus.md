# HTB Sherlock: Brutus #
In this very easy Sherlock, you will familiarize yourself with Unix auth.log and wtmp logs. We'll explore a scenario where a Confluence server was brute-forced via its SSH service. After gaining access to the server, the attacker performed additional activities, which we can track using auth.log. Although auth.log is primarily used for brute-force analysis, we will delve into the full potential of this artifact in our investigation, including aspects of privilege escalation, persistence, and even some visibility into command execution.

## Task 1: Analyze the auth.log. What is the IP address used by the attacker to carry out a brute force attack? ##
Upon opening the log, I noticed multiple failed login attempts to the admin user. This made the attacker's method, brute forcing, a dead giveaway. This also made it extremely easy to spot the attacker's IP address, which in this case, is 65.2.161.68.

<img src="https://i.imgur.com/8qG2nCC.png" width="750" height="250">

## Task 2: The bruteforce attempts were successful and attacker gained access to an account on the server. What is the username of the account? ##
Scrolling through the log, the attacker seemed to traverse through multiple user accounts and brute forcing every single one of them. One of these user accounts ended up becoming successful, and we can see this in auth.log as sshd accepts a password attempt to the user "root", as well as creating a new session for this specific user.

<img src="https://i.imgur.com/0tFcylS.png" width="750" height="50">

## Task 3: Identify the UTC timestamp when the attacker logged in manually to the server and established a terminal session to carry out their objectives. The login time will be different than the authentication time, and can be found in the wtmp artifact. ##
This task requires a different approach, as we cannot use a simple program like Notepad++ or Geany to analyze a binary file like wtmp. Since this binary file is a wtmp file, however, we have the ability to utilize utmpdump to dump and print the contents of the file at our disposal.
As I am using the Tsurugi Linux environment that I created from my DFIR project, I simply navigated to my downloads folder through the linux terminal and used utmpdump on the wtmp file that was provided to use from the Brutus.zip file provided to us at the beginning of the box.

<img src="https://i.imgur.com/XvAuZR3.png" width="500" height="50">

From here, we're able to get the log of the entire terminal session...

<img src="https://i.imgur.com/jzUGCF1.png" width="1000" height="500">

...including the time when the atttacker established the terminal session!

<img src="https://i.imgur.com/bGGkQIG.png" width="1000" height="15">

## Task 4: SSH login sessions are tracked and assigned a session number upon login. What is the session number assigned to the attacker's session for the user account from Question 2? ##
This task only requires us to analyze the same lines of the log from task 2, which gives us the session number we need for this question.

<img src="https://i.imgur.com/9ey1s74.png" width="750" height="50">

## Task 5: The attacker added a new user as part of their persistence strategy on the server and gave this new user account higher privileges. What is the name of this account? ##
Following the lines from Task 4, we notice a little further below that new groups and users were added to the server under the same IP address used for the attack. 

<img src="https://i.imgur.com/BkYzCse.png" width="1000" height="100">

## Task 6: What is the MITRE ATT&CK sub-technique ID used for persistence by creating a new account? ##
Since we know that the attacker used a persistence technique which involved creating a new user account, we can pinpoint to the "Create Account" persistence technique to find the correct sub-technique, and since we know that the server we are analyzing is a local server, we can pinpoint that the subtechnique used for this attack is the Local Account subtechnique.

<img src="https://i.imgur.com/MOJfJhl.png" width="1000" height="250">

## Task 7: What time did the attacker's first SSH session end according to auth.log? ##
Since we know that the attacker used the root user on session number 37, we want to find the first disconnect from user root and session 37. Once the lines have been found, all we need to do is locate the time that this session ended, which is at the leftmost side of the log.

<img src="https://i.imgur.com/ZeVbQq3.png" width="1000" height="100">

## Task 8: The attacker logged into their backdoor account and utilized their higher privileges to download a script. What is the full command executed using sudo? ##
A little after the first SSH session was closed, the attacker then created another session, but for his own user this time. With this user, the attacker used curl to download a malicious script on the HTTPS protocol. 

<img src="https://i.imgur.com/qYFe5QS.png" width="1000" height="35">

## Conclusion ##
This box was a great introduction to the Sherlock boxes available on HackTheBox. This basic challenge taught me how to identify many things in server logs, such as how to find the date and time of an attack, identifying an attacker's IP address and the user they compromised, as well as their attack method, which will help me learn how to identify indicators of compromise throughout the future boxes, and also throughout my DFIR project.

<img src="https://i.imgur.com/XdqG5su.png" width="500" height="500">
