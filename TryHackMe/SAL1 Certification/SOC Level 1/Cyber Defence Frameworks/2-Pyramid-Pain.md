# Pyramid of Pain
Basic concept as Security Analyst

## Hash Values
Numeric value of fixed length to uniquely identify data. Result of a hashing algorithm. Most common are:

* **MD5(Message Digest):** 128-bit hash value. Not cryptographically secure. Hash collision, attack against it.
* **SHA-1(Secure Hash Algorithm 1):** 160-bit hash value string as 40 digit hexadecimal number. NIST deprecated its use in 2011 and banned it from digital signatures due to brute-force attacks.
* **SHA-2:** Many variants. SHA-256 is most common which has a value of 256-bits as a 64 digit hexadecimal number.

Hash value to get insight into a malware sample, malicious file.
Tools for hash lookups: [Virustotal](https://www.virustotal.com/gui/home/upload), [Metadefender Cloud](https://metadefender.opswat.com/)

A hash in our arsenal helps in spotting a malicious file. However, we must be aware that attackers can modify the file for a single bit and it alters totally the hash value and threat hunting using file hashes as IOC can be difficult.

## IP Address
Used to identify any device connected to a network. IP address are used as an IoC. If recognised as malicious it is used to block, drop or deny inbound requests on the firewall. A way to challenge the IP blocking is through Fast Flux.

## Domain Names
Mapping an IP address to a string of text. We have top-level (evilcorp.com) or a sub-domain followed by the top-level one (tryhackme.evilcorp.com). A common attack is Punycode -> Cnverting words that cannot be written in ASCII to a Unicode ASCII encoding. To detect malicious domains we can use logs from web servers and proxies.

In addition, attackers hide malicious domains under URL shorteners. This is a tool to create a short and unique URL and redirect traffic to a specific website. Here is a list:

    bit.ly
    goo.gl
    ow.ly
    s.id
    smarturl.it
    tiny.pl
    tinyurl.com
    x.co

## Host Artifacts
Traces/Observables that attackers leave on the system.
* Registry values.
* Suspicious process execution.
* Attack patters.
* Files dropped.
* IoCs.

## Network Artifacts
If you can detect and respond the threat, the attack might need to go back and change his tactics, tools, procedures, etc.
* User-agent string.
* C2 info.
* URI patters followd by the HTTP POST requests.

They can be detected in PCAPs using Wireshark, Tshark or exploring IDS logs.

## Tools
* Attacker most likely give up.
* Some good alternatives are: Antivirus signatures, detections rules, and YARA rules.
* You have MalwareBazaar and Malshare to access samples, feeds and YARA results.
* For detections rules, SOC Prime Threat Detection Marketplace.
* Fuzzy hasing other weapon against attacker's tools. It helps performing similarity analysis, matching two files with minor differences based on fuzzy hash values. A tood is SSDeep. CTPH (Context Triggered Piecewise hashes).

## TTPs
* Whole MITRE ATT&CK Matrix. Therefore, all steps taken by adversary to achieve its goal.

