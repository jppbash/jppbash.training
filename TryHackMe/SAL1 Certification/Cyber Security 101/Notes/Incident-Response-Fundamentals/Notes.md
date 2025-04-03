# Incident Response (IR) Fundamentals

## Introduction

As human beings we are used to make decisions regarding preventative protection of our assets. For example, I live in Ecuador and currently the country is not safe. I am glad I drive a car and feels more secure but regardless. Now there are CCTVs everywhere, a group of guards where I live to protect the main entrances to the flat and the parking lot. However, what if an attacker/criminal figures out the way to bypass all those controls? Therefore, we must also take measures after the attack. 

Under the technology context, we hear about cyber attacks or read them in posts such as The Hacker News, Darknet Diaries and so on. We get to know about financial loses, trust rupture. These events are what we commonly know as **Cyber Security Incidents**.

Incident Response (from now on IR) is about handling an incident from its beginning to the end. It is about deploying security in different areas to prevent incidents or also to change the current control in order to contain it and prevent further damage. In risk terms, **minimise the impact**. IR is about guidelines and vary according to the organisation's policies, procedures as well as infrastructure. From endpoints to security solutions.

### Learning Objectives

* Overview of what are incidents and their severity levels
* Common types of incidents
* Phases of IR from SANS and NIST Frameworks
* Tools for Incident Detection and Response along with the role of PlayBooks
* Incident Response Plan (IRP)

## What is an incident?

To understand about IR it is important to known what is actually an incident. For this let's think about the following: Nowadays computers send loads of events daily. From an interactive process like watching a stream on Twitch, right? But we have also the non-interactive ones like background processes. I invite you to open the Task Manager in your Windows Computer or use the `top` command in a Linux machine. You will see some activities that you as a user, have not summoned. In a centralised security solution like a SIEM, we send these events as a log, and the security solutions can find whether it is harmful or not. But hang on, the real challenge is after the security solution points these activities out.

We receive an alert from the security solution. This is because it finds that a group of events might be related to a potential harmful activite. This is where the **Security Analyst** comes to action. Some alerts might be a **False Positive (FP)** or a **True Positive (TP)**. When an alert points to something dangerous but in fact, it is not harmful, we are talking about a FP. Otherwise, an alert that points to something dangerous, it is analysed and indeed it is, we are talking about a TP. Let's check the following examples:

**False Positives (FP):**
1. A security solution flags a legitimate software update process as malicious because it detects unusual network activity. Upon investigation, it turns out to be a routine update from a trusted vendor.
2. An employee accesses a file-sharing service for work purposes, but the security system raises an alert for potential data exfiltration. After review, it is confirmed that the activity was authorized by the senior manager and there is an email confirming the authorisation.

**True Positives (TP):**
1. A security alert identifies a phishing email containing a malicious link. Upon analysis, it is confirmed that the link leads to a credential-stealing website.
2. A detection system flags unusual login attempts from multiple geographic locations within a short time frame. Investigation reveals that an attacker is attempting to execute a brute-force attack from multiple sources to bypass somo wrong credential login policies.

With this, we can conclude that a TP alert can be referred to as **Incidents**. If the alert is classified as incident, the next phase is to assign a security/risk level. This is because Security teams get multiple incidents at the same time. Therefore, which one are you giving priority? The higher the risk, the higher the priority for its attandance and appropriate measures to contain and migitate.

## Types of Incidents

Most people might label/frame a harmful activity as a hacking attempt. Sometimes it is correct but as future Security Professional, we must be aware that there are multiple types of cyber attaacks. In addition, some of them can be accidental, otherwise what about intended ones? And not necessarily external attacks, what about insider threats? That is the reason why the Analyst and the DFIR teams should work in tandem to figure out the root cause of the incident. We must find out **WHO DID IT**. Now let's dicuss some types of incidents:

* **Malware:** Malicious programs that can damage a system, newtork or application. Besides there are different types of malware, each one with a different scope. We are looking for executable files, text files, documents, maybe a process running on the background making the computer perform slower.
* **Security Breaches:** It is about unauthorised access to confidential data. Log reading is important for this. Think about whether it is transferred to an external C2 server, done from the intranet by a disgruntled employeed.
* **Data Leaks:** It is about the exposure of confidential information. This is something that damages the reputation of the organisation. But remember one thing, unlike a security breach, this can also be cause by a misconfiguration. Therefore, human error is a factor to have in consideration when investigating the incident.
* **Insider Attacks:** This is something we must pay loads of attention because a disgruntled employee, has access to the internatl network and therefore, to some sensitive assets. The damage can be unmeasurable.
* **Denial of Service (DoS) Attacks:** Availability is important in this field and let's be realistic. What is the point of having protection and several controls to our assets if the system is not available. As simple as that.

## Incident Response Process

As seen above, there are loads of security incidents and therefore, we need a structured process for IR. Frameworks such as SANS and NIST are helpful for this situation. 

### Comparison of NIST and SANS Incident Response Frameworks

| **Aspect**                | **NIST Framework**                                                                 | **SANS Framework**                                      |
|---------------------------|------------------------------------------------------------------------------------|-------------------------------------------------------|
| **Phases**                | 1. Preparation<br>2. Detection and Analysis<br>3. Containment, Eradication, Recovery<br>4. Post-Incident Activity | 1. Preparation<br>2. Identification<br>3. Containment<br>4. Eradication<br>5. Recovery<br>6. Lessons Learned |
| **Focus**                 | Emphasizes a structured approach to incident handling with detailed documentation and analysis. | Focuses on practical steps for immediate response and recovery. |
| **Preparation Phase**     | Includes creating policies, procedures, and training for incident handling.         | Similar focus on readiness but emphasizes tools and resources for response. |
| **Identification** | Combines detection and analysis into a single phase to identify and understand incidents. | Separates identification as a distinct phase to focus on recognizing incidents. |
| **Containment**           | Part of a combined phase with eradication and recovery, focusing on limiting damage. | A standalone phase, emphasizing immediate actions to isolate the threat. |
| **Eradication and Recovery** | Combined into a single phase to remove threats and restore systems.                 | Treated as separate phases to ensure thorough removal and system restoration. |
| **Post-Incident Activity**| Focuses on lessons learned, documentation, and improving future response strategies. | Similar focus but referred to as "Lessons Learned" with an emphasis on team debriefing. |
| **Use Case**              | Suitable for organizations requiring detailed documentation and compliance.         | Ideal for teams needing a straightforward, action-oriented approach. |

Both frameworks provide valuable guidance for incident response, and organizations may choose one or combine elements of both based on their specific needs.

### Detailed Comparison of NIST and SANS IR Frameworks with Examples

| **Phase**                  | **NIST Framework**                                                                 | **SANS Framework**                                      | **Examples**                                                                 |
|----------------------------|------------------------------------------------------------------------------------|-------------------------------------------------------|------------------------------------------------------------------------------|
| **Preparation**            | Focuses on creating policies, procedures, and training for incident handling.      | Emphasizes readiness with tools, resources, and training for response.      | Conducting regular security awareness training and creating an IR playbook. |
| **Identification** | Combines detection and analysis to identify and understand incidents.             | Separates identification to focus on recognizing incidents.                 | SIEM alerts flagging unusual login attempts or malware detection.           |
| **Containment**            | Part of a combined phase with eradication and recovery, focusing on limiting damage. | A standalone phase emphasizing immediate actions to isolate the threat.     | Isolating an infected endpoint from the network to prevent malware spread.  |
| **Eradication**            | Combined with recovery to remove threats and restore systems.                      | A distinct phase ensuring thorough removal of threats.                      | Removing malware from an infected system and patching vulnerabilities.      |
| **Recovery**               | Combined with eradication to restore systems to normal operation.                  | A separate phase focusing on restoring systems and verifying functionality. | Restoring data from backups and verifying system integrity post-incident.   |
| **Post-Incident Activity** | Focuses on lessons learned, documentation, and improving future response strategies. | Referred to as "Lessons Learned," emphasizing team debriefing and improvement. | Conducting a post-incident review to identify gaps in the response process. |

This table highlights how each phase aligns between the frameworks and provides practical examples for better understanding.

## Incident Response Techniques

This section discusses aabout some solutions used for the IR process. Some of them have the capability of detection while others can also respond and execute other phases such as containment, eradication, etc. Let's discuss briefly some solutions:

* **SIEM:** It collects logs in a centralised environments for its correlation fto identify incidents.
* **Antivitus (AV):** Detects maliccious programs on endpoints and regularly scans the system.
* **EDR:** Deployed on every system to protect it against advanced-level threats. This can also contain and eradicate the threat.

We must be aware that procedures must be followed once an incident has been detected. The steps may vary depending on the kind of incident. These type of instructions are known as **Playbooks.**

## Conclusion

This documentation presents some concepts related to incident response. It mentions the importance of categorising events as TP, FP and also setting up priorities based on risk levels. In addition, it was reviewed the SANS and NIST frameworks as guideline to handling an incidents.