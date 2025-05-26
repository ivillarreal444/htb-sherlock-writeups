# HTB Sherlock: ElectricBreeze-1 #
Your security team must always be up-to-date and aware of the threats targeting organizations in your industry. As you begin your journey as a Threat Intelligence Intern, equipped with some SOC experience, your manager has assigned you a task to test your research skills and how effectively you can leverage the MITRE ATT&CK framework. * Conduct thorough research on Volt Typhoon. * Use the MITRE ATT&CK framework to map adversary behavior and tactics into actionable insights. Impress your manager with your assessment, showcasing your passion for threat intelligence.

**[ KEY INFORMATION ](https://attack.mitre.org/groups/G1017/)**

# Task 1: Based on MITRE's sources, since when has Volt Typhoon been active? #
Using the key information above, based on MITRE's summary of the threat actor, this group has been around since at least 2021.

<img src="https://i.imgur.com/0VpXZiG.png" width="1000" height="250">

# Task 2: MITRE identifies two OS credential dumping techniques used by Volt Typhoon. One is LSASS Memory access (T1003.001). What is the Attack ID for the other technique? #
Not only has Volt Typhoon used the LSASS Memory acccess technique, but they have also utilized the NTDS technique (T1003.003), which utilizes ntds.util to create installation media for the organization's domain controller, this installation media containing the username and password hashes stored in the domain controller.

<img src="https://i.imgur.com/mZR8YPs.png" width="1000" height="100">
