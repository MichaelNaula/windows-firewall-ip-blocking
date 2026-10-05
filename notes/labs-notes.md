**Windows Firewall Website/IP Blocking Lab — Lab Notes
Lab Information**
Project: Windows Firewall Website/IP Blocking Lab
Target Website: Facebook (facebook.com)
Operating System: Windows
Firewall: Windows Defender Firewall with Advanced Security
Firewall Direction: Outbound
Rule Type: IP-based blocking
Date: 10/05/2026

**Step 1 — Find the Website IP Address**
I opened Windows Command Prompt and ran: ping facebook.com
Result
The command successfully resolved facebook.com to an IPv4 address.
IPv4 address returned: 157.240.9.35
Screenshot
 

**Step 1B — DNS Lookup Using nslookup**
I also used the following command: nslookup facebook.com
Result
The nslookup command displayed DNS information for facebook.com.
IPv4 address observed: 157.240.9.35
Screenshot
 
**Observation**
The ping and nslookup commands demonstrated how a domain name can be resolved to an IP address.
The domain name is easier for humans to remember, while the IP address is used for network communication.
Step 2 — Test Facebook Before Blocking
Before creating the firewall rule, I opened Facebook in a web browser.
Website: https://www.facebook.com
Result Facebook was: Reachable

**Observation**
This test established the baseline condition before the firewall rule was created.
Screenshot
 

**Step 3 — Open Windows Defender Firewall**
I opened Windows Defender Firewall with Advanced Security by using: wf.msc
Screenshot:
 

I then selected: 
Outbound Rules:
•	New Rule
Rule Configuration:
Rule type:
•	Custom
Program:
•	All programs
Remote IP address:
157.240.9.35
Action:
•	Block the connection
Rule name:
•	Block Facebook IP
Screenshot
 
**Step 4 — Verify the Firewall Rule**
After creating the rule, I opened the rule's properties.
The rule was configured with:
Action: Block the connection
The rule targeted the remote IP address obtained during the DNS resolution step.
Screenshot
 
Observation
The firewall rule was successfully created and enabled.
The purpose of the rule was to prevent outbound traffic matching the specified remote IP address.

**Step 5 — Test After Enabling the Firewall Rule**
I attempted to access Facebook again after enabling the firewall rule.
Result
Facebook was: BLOCKED
Observation
After the firewall rule was enabled, access to Facebook was blocked during my test.
This demonstrated that the firewall rule was affecting traffic to the selected IP address.
However, this does not mean that blocking one IP address will always block an entire website. Websites can use multiple IP addresses and distributed infrastructure.
Screenshot
 
**Step 6 — Disable the Firewall Rule**
I disabled the firewall rule instead of deleting it.
This allowed me to keep the rule configuration while preventing it from actively blocking the matching traffic.
Rule Status: Disabled 
I then attempted to access Facebook again.
Result
Facebook was: REACHABLE
Observation
I was able to log in to the website because the IP blocking has been disabled.
Screenshot:
 
**Step 7 — Main Observations**
During the lab, I observed the following:
1.	A domain name can be resolved to an IPv4 address using DNS.
2.	Windows Firewall can create outbound rules based on remote IP addresses.
3.	A firewall rule can block traffic matching the specified IP address.
4.	Disabling the firewall rule stops that rule from actively blocking the matching traffic.
5.	Blocking one IP address does not necessarily mean that every connection to a website will be blocked.
6.	Large websites can use multiple IP addresses and distributed network infrastructure.



**Step 8 — Cybersecurity Concepts Learned**
DNS Resolution
DNS translates human-readable domain names into IP addresses.
Example:
facebook.com --> IPv4 address
This allows computers to locate network destinations using IP addresses.
IPv4
IPv4 provides numerical addresses used to identify network endpoints.
Example format: 192.0.2.1
The actual address used in this lab was obtained through my own DNS lookup.
Outbound Traffic
Outbound traffic is traffic leaving my windows computer. The firewall rule created in this lab controlled outbound traffic destined for a particular remote IP address.
Windows Firewall
Windows Defender Firewall is a host-based firewall that can control network connections using configurable rules.
Firewall rules can use conditions such as:
•	Program
•	Protocol
•	Local IP address
•	Remote IP address
•	Local port
•	Remote port
•	Network profile



IP-Based Blocking
The rule in this lab was based on a specific remote IP address. The firewall does not simply block the text; facebook.com. Instead, it evaluates network traffic and determines whether it matches the conditions defined by the firewall rule.

**Step 9 — IP Blocking vs. Domain Blocking**
The lab demonstrated that IP blocking and domain blocking are different concepts.
The basic process is:
facebook.com
      
      
DNS resolution--> IP address-->Firewall rule-->Traffic blocked
If the domain uses another IP address, traffic to that other address may not match the firewall rule.




**Step 10 — Limitations**
Multiple IP Addresses
A domain can have multiple IP addresses. Therefore, blocking one IP address may not block every connection to the website.
Changing DNS Results
DNS results can change over time. A domain may resolve to a different IP address later.
Distributed Infrastructure
Large websites can use servers and network infrastructure distributed across different locations.
Shared IP Addresses
An IP address may potentially be associated with more than one service. Blocking an IP address can therefore have unintended effects.
IP Blocking Is Not Domain Blocking
The firewall rule created in this lab targeted an IP address. It did not create a general rule that understands or blocks every request for the domain name facebook.com.

**Step 11 — Problems or Challenges**
During the lab, I encountered the following problems:
•	I initially entered an incorrect IP address and had to verify the address before testing the connection again.
•	I initially struggled to navigate the firewall management interface but became more familiar with it after reviewing the available settings.

**Step 12 — Final Result**
Before Blocking
Facebook: Reachable
After Enabling Firewall Rule
Facebook: Unreachable
After Disabling Firewall Rule
Facebook: Reachable

**Step 13 — Final Reflection**
This lab helped me understand how Windows Defender Firewall can be used to control outbound network traffic.
The main lesson I learned is that blocking an IP address is not necessarily the same as blocking a website. Modern websites can use multiple IP addresses and distributed infrastructure, so blocking a single IP address may only affect some of the traffic associated with the website.
I also learned how DNS resolution connects a human-readable domain name to an IP address and how firewall rules can use that IP address as a condition for controlling network traffic.

