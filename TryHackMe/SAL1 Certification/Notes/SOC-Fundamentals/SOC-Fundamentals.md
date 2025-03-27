# SOC Fundamentals

Main focus of SOC team is **Detection and Response**. SOC team has resources in manner of security solutions for the achievement of both above. It integrates network and all systems to monitor from a centralised location. This is paramount for the detaction and response to any incident.

### Detection
* **Vulnerabilities:** It is not necesarrily the SOC's reponsibility regardless, it still affects the security level of the organisation.
* **Unauthorised activity:** An example is that an attacker discovered the username and password of an employee. We must detect this before it causes some further damage.
* **Policy violations:** A policy is a set of rules and procedures created for security compliance as well as against threats. Proceeding against it is considered a violation and varies from company to company.
* **Intrusions:** It is referred to unauthorised access to systems and networks. What about an attacker exploting your web application, or visiting a malicious site and getting the computer infected, for instance?

### Response
* **Support with Incident Response:** When an incident is detected, there are certiain steps for its response. It includes minimising damage, therefore impact and finding the root cause as an analysis of the incident. SOC teams helps the IR team for this. 

In addition, there are three pillars in SOC which are **People, Proceess and Technology**. They must coexist because a team of professional people working on state-of-art security tools together with proper processes makes a mature SOC environment.

## People

We must understand that despite the constant technological evolution, **people in a SOC will always be important.** A security solution can create various red flags in a SOC environments, imagine the noise that can provoke numerous ones connected at the same time.

If there is no human intervention in a SOC environment, it is most likely you will focus on irrelevant issues. People helps the security solution to truly identiy potential harmful activities and enable a proper response. People is known in a SOC team, having the following roles and responsibilities:

![](/TryHackMe/SAL1%20Certification/Notes/SOC-Fundamentals/Fig1-Roles.png)

* **SOC Analyst (Level 1):** First responders to any detection. Basic alert triage and reporting through proper channels.
* **SOC Analyst (Level 2):** Dive deeper into investigations and correlate data from multiple sources.
* **SOC Analyst (Level 3):** Experienced professionals looking for threat indicators and support in IR activities. Critical detection reports from tier 1 and 2 are often incidents with the requirements of detailed responses including containment, eradication and recovery.
* **Security Engineer:** Deployment and configuration of security solutions for smooth operation
* **Detection Engineer:** Rules are built behind security solutions to detect harmful activities. Created normally by Tier 2 and 3 Analyst but this role can take full responsibility in an independant manner. 
* **SOC Manager:** Manages processes of the SOC team and provides supports. Remains in contact with the organisation's CISO to provide him with updates on the SOC team's posture and efforts.

Roles can increase/decrease depending on size and criticality of organisations.

## Process
Each role has its own processes. Let's discuss some important processes involved in a SOC.

### Alert Triage
Basis of SOC team. First reponse to any alert. Focused on analysing the specific alert, determining its severity and helps in the priorisation. It answers the 5 Ws as shown below.

![](/TryHackMe/SAL1%20Certification/Notes/SOC-Fundamentals/Fig2-Alert-Triage.png)

**Alert:** Ransomware detected on host **WINSERVER2022-MAIN-VLAN20**

<div align="center">

| W              | Answer                                      |
|-----------------|---------------------------------------------|
| Who            | WINSERVER2022-MAIN-VLAN20                  |
| What           | Ransomware detected                        |
| When           | Time of detection (e.g., 2023-10-05 14:30) |
| Where          | Main VLAN 20                               |
| Why            | Possible malicious file execution          |

</div>

### Reporting
Alerts must be escalated to higher-tier analysts for a timely and appropriate response and resolution. They are escalated as tickets and assigned to the revelant people. It includes the 5Ws with a thorough analysis as well as screenshots as evidence of the activity.

### Incident Response and Forensics
Reported detections can pinpoint to highly malicious activiites classified as critical. In those kind of situations, high-tier teams start an IR process. Sometimes, forensics activities might need to be executed. This aims to determine the incident's root cause by analysing artifacts from a system/network.

## Technology
This refers to the security solutions used in the organisation and they effectively minimise the SOC team's effort to detect and respond to threats. 

An organisation's network may have many devices and applications. Detecting and responding individually means loads of effort and resources. Security solutions centralise information automating the detection and response capabilities. Let's discuss some of these solutions:

* **SIEM:** Security Information and Event Management (SIEM) is a popular tool in a SOC environment. Collects logs from various network devices. Detection rules are configured in the SIEM solution with the corresponding logic to identify suspicious activity. Modern SIEM solutions provide nowadays user behaviour analytics and threat intelligence capability. ML algorithms support the enhancement of the detection capabilities.

**Note:** SIEM only provide **Detection** capabilities

* **EDR:** Endpoint Detection and Response (EDR) provide detailed real-time and historical visibility of devices' activities. Operates on endpoint level and can carry out automataed responses. Has extensive detection capabilities, allowing the investigation in detail and response with just few clicks.
* **Firewall:** Works purely for network security acting as barrier (door) between internal and external network. It monitors incoming and outgoing network traffic and filters unauthorised traffic. It also has some detection rules deployed for the identification and blocking of suspicious traffic.

There are other security solutions such as AntiVirus, [EPP]([EPP](https://www.gartner.com/en/information-technology/glossary/endpoint-protection-platform-epp)), IDS/IPS, XDR, SOAR, etc.

# Practical Exercise of a SOC

## Scenario

You are the Level 1 Analyst of your organization’s SOC team. You receive an alert that a port scanning activity has been observed on one of the hosts in the network. You have access to the SIEM solution, where you can see all the associated logs for this alert. You are tasked to view the logs individually and answer the question to the 5 Ws given below.

**Note:** The vulnerability assessment team notified the SOC team that they were running a port scan activity inside the network from the host: 10.0.0.8

### Answer questions below

**What: Activity that triggered the alert?**

* A port scan. The vulnerability assessment team made that notification therefore it is important to have that in mind while doing the rest of analysis of the alert.

**When: Time of the activity?**

* June 12, 2024 17:24

**Where: Destination host IP?** 

* 10.0.0.3

**Who: Source host name?**

* Nessus

**Why: Reason for the activity? Intended/Malicious**

* This is intended because of the notification from the VA team

**Additional Investigation Notes: Has any response been sent back to the port scanner IP? (yea/nay)**

* Yes because there was a response from the destination host IP presenting an open port. It was in fact the SSH port which can lead to a remote access.

**What is the flag found after closing the alert?**

* THM{000_INTRO_TO_SOC}

## Conclusion

This course helped understanding the architecture of a SOC, including its pillars, roles, responsibilities and scope of each. In addition, there was the chance to analyse an event even though it was a false positive. However, that is part of the Security Analyst, to discard as mucha false positives as possible to focus on relevant issues for its proper detection and avoid an incident that might require the escalation to high-tier analysts or even the SOC Manager following the "chain of command". Huge thanks to TryHackMe for offering great content and hands-on experience.