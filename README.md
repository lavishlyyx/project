<img width="750" height="398" alt="image (3)" src="https://github.com/user-attachments/assets/e30b2211-b312-44ca-9e7f-7d7adc8c5292" />Active Directory Proeject

Active Directory is a centralized database that stores and manages information about users, computers, and groups within a network. It allows administrators to organize and control access to network resources. To use Active Directory, a server must have the Active Directory Domain Services (AD DS) role installed and then be promoted to a Domain Controller. Once promoted, the server can handle authentication using the Kerberos protocol and manage authorization by applying policies and permissions across the domain.

During this project, I also had to troubleshoot several issues while setting up and connecting systems. These included fixing network configuration problems, adjusting static IP settings, resolving domain join errors, and ensuring that services like DNS and AD DS were running properly. These troubleshooting steps helped deepen my understanding of how Active Directory functions and how to solve real-world problems in a networked environment.

![image-alt](https://github.com/lavishlyyx/project/blob/c31f5ad4123f17a56c687fb861fa8d79f10c4722/Screenshot%202026-06-18%20201023.png)

Lab Setup and Planning

To get started, I created a basic network diagram using draw.io
This helped me plan out how all the parts of my lab would connect and work together.

My lab included:

> Windows Server — this was my domain controller that ran Active Directory.

> Windows 10 PC — a regular computer that would join the domain.

> Kali Linux — used to test security by trying different attacks.

> Splunk Server — collected and showed logs from other devices.

> Splunk Universal Forwarder — sent logs from Windows machines to Splunk.

> Sysmon — added extra logging on Windows to track system activity.

> Router and Internet — used to simulate a real network.

This diagram made it easier to understand what I needed and how each machine would talk to the others.

<img width="750" height="406" alt="zakaria_virtualbox_ad_lab" src="https://github.com/user-attachments/assets/c6d49a53-64a8-4e95-be74-d4f7da2f14dd" />

<img width="786" height="410" alt="image (3)" src="https://github.com/user-attachments/assets/5bf1445b-96c7-4611-a384-aa550216f164" />


Virtual Machine Setup
I used Oracle virtual box to install four virtual machines on my computer, each with a different role

Windows 10 was the target machine, acting like a regular user computer.

Kali Linux was the attacker machine, used for testing and hacking tools.

Windows Server 2022 was set up to run Active Directory, which manages users and network rules.

Ubuntu Server ran Splunk, which collects and shows logs from all machines.
What is Active Directory?

(Active directory) is a system that helps manage users, computers, and access in a network.

It uses AD DS (Active Directory Domain Services) to store a database of objects like users, computers, and groups.

Each object has attributes, which are pieces of information such as names, passwords, and roles.

In short:

>Windows 10 = target
Kali Linux = attacker

>Windows Server 2022 = runs Active Directory

>Ubuntu Server = runs Splunk

>All of this was set up using VirtualBox for safe testing.


<img width="1908" height="1021" alt="image (4)" src="https://github.com/user-attachments/assets/6744d7e4-e7d8-482f-8903-70f27a14a4e0" />


<img width="1100" height="589" alt="image (5)" src="https://github.com/user-attachments/assets/5e65a176-b1ed-4fac-94e4-29033f3d062f" />

<img width="750" height="388" alt="image" src="https://github.com/user-attachments/assets/8aa61eb0-7004-48db-99e2-0b2329d4a6c9" />

<img width="750" height="394" alt="image (6)" src="https://github.com/user-attachments/assets/0e38aaed-a895-4e2a-bd6e-3a74a984fd22" />


Setting Up Splunk on Ubuntu Server
To set up Splunk on the Ubuntu Server, I first installed VirtualBox Guest Additions so I could use a shared folder between my host computer and the Ubuntu virtual machine. This made it easier to move files. After that, I created a new Netplan configuration file to give the Ubuntu server a static IP address. This was important so that both the Windows 10 target machine and the Windows Server 2022 could reliably connect to it over the network.

Installing Sysmon and Splunk Forwarder
On the Windows 10 machine, I accessed the Splunk web interface by logging into my Splunk account using the server’s IP address. Then I installed Sysmon with a custom configuration file I found on GitHub. Before installing Sysmon, I had to download and install the Splunk Universal Forwarder. I edited the inputs.conf file so that all the logs from Sysmon would be sent to the Splunk server. I repeated this process on the Windows Server 2022 as well, so that both machines would forward their data.

Final Setup
After completing the setup on both machines, I was able to start seeing incoming data in my Splunk server. I created a new index named “Endpoint” where all the logs were stored. These logs included system activity from both the Windows 10 target machine and the Windows Server 2022. I could now view detailed information such as process creation, network connections, and other useful events collected by Sysmon.


Thanks to the static IP setup, the Splunk Forwarders on both machines were able to send data without any connection issues. This setup allowed me to monitor the behaviour of both systems in real time and made it easier to track anything suspicious or unusual happening in the network. My home lab environment is now able to log and analyse activity across all connected virtual machines through Splunk.



<img width="640" height="340" alt="image (3)" src="https://github.com/user-attachments/assets/540a6cd7-2545-4d98-ac8b-2fd095f53d6f" />
<img width="592" height="439" alt="image (4)" src="https://github.com/user-attachments/assets/de4f5b83-2b00-4ece-b719-8b5451de559d" />
<img width="582" height="439" alt="image (5)" src="https://github.com/user-attachments/assets/62f15c8f-b59d-46ef-a9bf-37f03e812e23" />




Using the Splunk Web Portal


After setting up the Splunk server on the Ubuntu machine, I opened a web browser and went to the address 192.168.10.10:8000. This took me to the Splunk web portal, where I logged in to access the dashboard. From here, I could manage data, view logs, and check if everything was working correctly.

Once I was inside the portal, I installed the Splunk Universal Forwarder on both the Windows 10 target machine and the Windows Server 2022. The forwarder is a tool that sends system logs to the Splunk server so I can view them all in one place. This step was important because without the forwarder, Splunk would not receive any data from those machines.

After setting up the forwarder, I moved on to installing Sysmon. Sysmon is a tool that watches what is happening on the system, such as programs starting, files being changed, or network connections being made. It gives a lot of detailed logs that are useful for security monitoring.

To make Sysmon work better, I also downloaded a special configuration file from GitHub called the Sysmon Olaf config. This file tells Sysmon exactly what to record and what to ignore, helping to reduce unnecessary logs and focus on important events. I used the same config on both the Windows 10 and Windows Server machines.

With the forwarder and Sysmon installed and configured, both machines began sending useful logs to my Splunk server, where I could see and analyse them in real time.



<img width="1448" height="1086" alt="3adf9942-2705-4bb5-bf85-635116e50493" src="https://github.com/user-attachments/assets/a00a1daa-2328-40c0-9c85-2741464c81fa" />
<img width="1448" height="1086" alt="278822c6-46d1-4bd5-84e0-94e1f806121d" src="https://github.com/user-attachments/assets/e63b5417-fc66-47ff-b596-433f1d77f132" />
<img width="1448" height="1086" alt="be1173fe-cce3-4db9-95de-8b017680b78d" src="https://github.com/user-attachments/assets/3c74b7bf-40e7-432e-996b-cf2c37b3d8e8" />
<img width="1448" height="1086" alt="ae7c4c6f-be10-404d-a31a-3398e802d366" src="https://github.com/user-attachments/assets/1d580b27-1355-4d92-aa23-3404647c41bb" />


Installing and Configuring Active Directory

The next step was to install and configure Active Directory on the Windows Server 2022. First, I set a static IP address for the server to 192.168.10.7 so it would have a fixed address on the network. Then, I added the Active Directory Domain Services (AD DS) role through the Server Manager. After the installation, I promoted the server to a domain controller and created a new domain named walid7866.local.

Once the domain was set up, I moved on to creating users in Active Directory. I opened the Active Directory Users and Computers folder and created two organizational units (OUs): IT and HR. Inside the IT OU, I created a user named Elias Hawthorne, and in the HR OU, I created a user named Harry Brook.

After that, I went to the Windows 10 target machine. I changed its network settings to connect to the walid7866.local domain. I used the credentials for Elias Hawthorne to authenticate and successfully joined the target machine to the domain.

Now, both the server and the target machine are part of the same domain, and I can manage users and settings from the domain controller.


<img width="750" height="398" alt="image (3)" src="https://github.com/user-attachments/assets/94a01707-ca5d-495d-aa3a-4de90ff5c5c5" />
<img width="750" height="393" alt="image (4)" src="https://github.com/user-attachments/assets/880fbc31-63a0-4f69-9c4b-cacd7b92e6cc" />
<img width="720" height="399" alt="image (3)" src="https://github.com/user-attachments/assets/c6478bec-4cef-42f8-a7f5-0ddcd8034f49" />
<img width="786" height="412" alt="image (4)" src="https://github.com/user-attachments/assets/d2c0f2a0-d638-4157-882e-f5f4d22ed834" />
<img width="649" height="241" alt="image (5)" src="https://github.com/user-attachments/assets/22db140a-ff2f-45bd-a223-2ce2befafa3a" />
<img width="640" height="342" alt="image (6)" src="https://github.com/user-attachments/assets/8ccbab99-8bdc-4f02-bada-dec57e475bba" />
<img width="593" height="348" alt="image (7)" src="https://github.com/user-attachments/assets/12f89e71-53b1-406b-9d2f-3cc0ed8074ec" />

<img width="720" height="583" alt="image" src="https://github.com/user-attachments/assets/6ff78dbb-36a4-4f5c-845e-b608646a8770" />






