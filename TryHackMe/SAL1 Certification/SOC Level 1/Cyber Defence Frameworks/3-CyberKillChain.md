# Cyber Kill Chain
* Military concept related to the structure of an attack. Target identification, decision and order to attack and finally, destruction.
* Helps to understand and protect against ransomware attacks, security breaches and APTs. Assess network/system security by identifying missing controls and closing certains gaps.
* You can recognise intrusion attempts and understand the intruder's goals and objectives.

## 1 - Reconnaissance
* Discovering and collecting information on system and victim.
* OSINT falls under this stage. Attackers need to study the victim by collecting every available piece of information on the company and its employees.

**Email Harvesting:** obtaining email addresses from public, paid or free services. It can be useful for a phishing attack. Some tools are theHarvester, Hunter.io, OSINT Framework.

* Social media e.g. Linkedin, Facebook, X, Instagram

## 2 - Weaponisation
* Weapon of destruction. Creation of a "weaponizer" that combines malware and exploit into a deliverable payload.
* Automated tools to generate the malware or refer to the DarkWeb to purchase it.
* Sophisticated authors or nation-sponsored APT groups would write their custom one.

**Examples**
* MS Office document with a malicious macro or VBA script.
* Malicious payload or sophisticated worm.
* C2 techniques.
* Backdoors.

## 3 - Delivery
* Method to transmit the payload/malware.
* Phishing emails.
* Infected USBs in public.
* Watering hole attacks -> compromising the website and then redirecting them to the malicious website of the attacker's choice. Aimed to a specific group of people.

## 4 - Exploitation
* Leveraging a vulnerability. After gaining access, attacker could exploit SW, systems or server-based vulnerabilities to escalate privileges or pivot through the network.
* Zero-day exploits.

## 5 - Installation
* Persistence. Reaccessing the system if there is detection, patching, etc.
* Persistent backdoors.
  * Web shells
  * Backdoor on victim machine
  * Create/Modify Windows services
  * Adding entry to "run keys" for malicious payload in registry or startup folder.
  * Timestomping -> avoid detection by forensic analyst. Modification of timestamps, modify, access, create and change times.

## 6 - Command and Control (C2)
* Remote control and manipulation of the victim.
* Also know as C&C or C@ Beaconing.
* Infected hosts will consistently communicate with the C2 server.
* IC was the traditional C2 channel used by attackers.
* Comon C2 channels: HTTP/80, HTTPS/443, DNS Tunneling.

## 7 - Actions on Objectives (Exfiltration)
* Collect credentials.
* Privilege escalation.
* Internal reconnaissance.
* Lateral movement.
* Collect/exfiltrate data.
* Delete backups/shadow copies. Shadow copy is from Microsoft to create backup copies.
* Overwrite/corrupt data.

