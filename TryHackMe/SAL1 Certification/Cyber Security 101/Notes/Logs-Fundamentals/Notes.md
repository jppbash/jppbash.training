# Logs - Fundamentals

## Introduction

Let's think about somehwere within a system where we can track an attack. This is what logs have. They are digital footprints left behind any activity, regardless ob being normal or malicious. 

### Use Cases of Logs

| **Use Case**                        | **Description**                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| Security Events Monitoring       | Logs help detect and monitor suspicious activities or unauthorized access.  |
| Incident Investigation and Forensics | Logs provide critical evidence to analyze and trace the root cause of incidents. |
| Troubleshooting                  | Logs assist in identifying and resolving system or application issues.      |
| Performance Monitoring           | Logs track system performance metrics to ensure optimal operation.          |
| Auditing and Compliance          | Logs ensure adherence to regulatory requirements and internal policies.     |

### Learning Objectives

After completing this room, you will learn about the following:

* The different types of logs
* How to analyze logs
* Analyzing Windows Event logs
* Analyzing Web Access logs

## Types of Logs

If you open the log file of a system, you see numerous events from different categories and you might get overwhelmed. Hence, the segregation of logs into multiple categories according to the type of information they provide.

Let's put an example, you have been asked to check successful logins from yesterday at a specific timestamp in Windows. For that, you just need to check the system's **Security Logs** since you are looking for successful authentication attempts.

| **Type of Log**         | **Usage**                                                                 | **Examples**                                      |
|--------------------------|--------------------------------------------------------------------------|--------------------------------------------------|
| Security Logs            | Track authentication attempts, access control, and security-related events. | Successful logins, failed logins, privilege changes. |
| System Logs              | Record events related to system operations and hardware.                 | System startup, shutdown, driver errors.         |
| Application Logs         | Monitor application-specific events and errors.                         | Application crashes, configuration changes.      |
| Network Logs             | Capture network activity and traffic patterns.                          | Firewall logs, DNS queries, packet captures.     |
| Access Logs          | Track HTTP requests and user interactions with web servers.             | Page visits, HTTP status codes, user agents.     |
| Audit Logs               | Provide a record of changes and actions for compliance purposes.        | File access, configuration changes, policy updates. |

**Note:** This is the most common types but there are other types of logs depending on the different applications and services they provide.

## Windows Event Log Analysis

Windows logs many of the activities that take place and these files are segregated with a specific category. Let's discuss the most crucial types of logs:

* **Application Logs:** Information related to applications running are logged here, including erros, warnings, compatibility issues, etc.
* **System Logs:** The OS has different operations running. Any information related to is logged here. It includes driver and hardware issues, startup and shutdown inforamtion as well as service information, etc.
* **Security Logs:** It records all security related activies, including user authentication, changes in user accounts, security policy changes, etc.

Windows has an application called **Event Viewer** where you can see activity records in a user-friendly GUI. 

The following picture shows a Windows Event Log and the following components are described below:

<div align="center">

![](/TryHackMe/SAL1%20Certification/Cyber%20Security%20101/Notes/Logs-Fundamentals/Logs-Fundamentals-Figure1.png)

</div>

1. **Description:** Details of activity.
2. **Log Name:** Log file name.
3. **Logged:** Time of activity.
4. **Event ID:** A unique identifier for a specific activity.

As a Security Analyst it is important to know some of the most common Event IDs in a Windows OS. Here I leave some of them

<div align="center">

| **Event ID** | **Description**                                                                 |
|--------------|---------------------------------------------------------------------------------|
| 4624         | Successful account logon.                                                      |
| 4625         | Failed account logon.                                                          |
| 4634         | Account logoff.                                                                |
| 4672         | Special privileges assigned to a new logon.                                    |
| 4688         | A new process has been created.                                                |
| 4720         | A user account was created.                                                    |
| 4722         | A user account was enabled.                                                    |
| 4723         | An attempt was made to change an account's password.                           |
| 4725         | A user account was disabled.                                                   |
| 4732         | A member was added to a security-enabled local group.                          |
| 4740         | A user account was locked out.                                                 |
| 4768         | A Kerberos authentication ticket (TGT) was requested.                          |
| 4769         | A Kerberos service ticket was requested.                                       |
| 4776         | The computer attempted to validate the credentials for an account.             |
| 4798         | A user's local group membership was enumerated.                                |
| 5140         | A network share object was accessed.                                           |
| 5145         | A file or folder was accessed on a shared folder.                              |

</div>

## Web Server Access Log Analysis

A website/application log file contains requests made by clients with information on the timeframe, IP address from sender, type of request and URL. For instance in an Apache web server the access log file is located in the directory: `/var/log/apache2/access.log`

Figure Pending

Now checking the structure of this log we have the following:

* **IP Address:** The IP address of the user WHO made the request. E.g. "127.16.100.1".
* **Timestamp:** Time when the request was done. E.g. "[11/Jun/2025:15:31:52]".
* **Request:** Details of the request done following the HTTP protocol.
  * **HTTP Method:** The action the website has to perform on the request. E.g. "GET".
  * **URL:** "/". The resource requested.
* **Status Code:** Response from the server. E.g. "200".
* **User-Agent:** Information about the OS, browser, etc., when making the request. E.g., “Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36”