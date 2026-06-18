# Active Directory Project

Active Directory is a centralized database that stores and manages information about users, computers, and groups within a network. It allows administrators to organize and control access to network resources. To use Active Directory, a server must have the Active Directory Domain Services (AD DS) role installed and then be promoted to a Domain Controller. Once promoted, the server can handle authentication using the Kerberos protocol and manage authorization by applying policies and permissions across the domain.

During this project, I also had to troubleshoot several issues while setting up and connecting systems. These included fixing network configuration problems, adjusting static IP settings, resolving domain join errors, and ensuring that services like DNS and AD DS were running properly. These troubleshooting steps helped deepen my understanding of how Active Directory functions and how to solve real-world problems in a networked environment.

![image-alt](https://github.com/lavishlyyx/project/blob/c31f5ad4123f17a56c687fb861fa8d79f10c4722/Screenshot%202026-06-18%20201023.png)

Lab Setup and Planning

To get started, I created a basic network diagram using draw.io
This helped me plan out how all the parts of my lab would connect and work together.

My lab included:

Windows Server — this was my domain controller that ran Active Directory.

Windows 10 PC — a regular computer that would join the domain.

Kali Linux — used to test security by trying different attacks.

Splunk Server — collected and showed logs from other devices.

Splunk Universal Forwarder — sent logs from Windows machines to Splunk.

Sysmon — added extra logging on Windows to track system activity.

Router and Internet — used to simulate a real network.

This diagram made it easier to understand what I needed and how each machine would talk to the others.
