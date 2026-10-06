Windows Firewall Website/IP Blocking Lab — Lab Notes
Lab Information

Project: Windows Firewall Website/IP Blocking Lab

Target Website: Facebook (facebook.com)

Operating System: Windows

Firewall: Windows Defender Firewall with Advanced Security

Firewall Direction: Outbound

Rule Type: IP-based blocking

Date: 06/10/2026

Step 1 — Find the Website IP Address

I opened Windows Command Prompt and ran the following command:

ping facebook.com

Result

The command successfully resolved facebook.com to an IPv4 address.

IPv4 address returned: 157.240.9.35

Screenshot:
![Ping result](../screenshots/01a-ip-address-ping.png)

Step 1B — DNS Lookup Using nslookup

I also used the following command:

nslookup facebook.com

Result

The nslookup command displayed DNS information for facebook.com.

IPv4 address observed: 157.240.9.35

Screenshot:
![Ping result](../screenshots/01b-ip-address-nslookup.png)

Observation

The ping and nslookup commands demonstrated how a domain name can be resolved to an IP address. A domain name is easier for people to remember, while an IP address is used to identify the network destination for communication.

Step 2 — Test Facebook Before Blocking

Before creating the firewall rule, I opened Facebook in a web browser.

Website: https://www.facebook.com

Result

Facebook: Reachable

Observation

This test established the baseline condition before the firewall rule was created.

Screenshot:
![Ping result](../screenshots/02-before-blocking.png)

Step 3 — Open Windows Defender Firewall

I opened Windows Defender Firewall with Advanced Security by using:

wf.msc

Screenshot:
![Ping result](../screenshots/03-opening-windows-firewall-with-advanced-security.png)

I then selected:

Outbound Rules → New Rule

Rule Configuration

Rule Type: Custom

Program: All programs

Remote IP Address: 157.240.9.35

Action: Block the connection

Rule Name: Block Facebook IP

Screenshot:

![Ping result](../screenshots/04-Block-Facebook-IP.png)

The rule was configured as an outbound firewall rule designed to block traffic matching the specified remote IP address.

Step 4 — Verify the Firewall Rule

After creating the rule, I opened the rule's properties to verify its configuration.

The rule was configured with:

Action: Block the connection

Remote IP Address: 157.240.9.35

Status: Enabled

The rule targeted the remote IP address obtained during the DNS resolution step.

Screenshot:

![Ping result](../screenshots/05-rule-properties.png)

Observation

The firewall rule was successfully created and enabled. Its purpose was to prevent outbound traffic matching the specified remote IP address.

Step 5 — Test After Enabling the Firewall Rule

After enabling the firewall rule, I attempted to access Facebook again.

Result

Facebook: Blocked / Unreachable

Observation

After the firewall rule was enabled, Facebook was inaccessible during my test. This demonstrated that the firewall rule was affecting traffic destined for the selected IP address.

However, blocking a single IP address does not necessarily block an entire website. Websites can use multiple IP addresses, load balancing, content delivery networks, and other distributed infrastructure.

Screenshot:

![Ping result](../screenshots/06-after-blocking.png)

Step 6 — Disable the Firewall Rule

Instead of deleting the firewall rule, I disabled it. This allowed me to keep the rule configuration while preventing it from actively blocking matching traffic.

Rule Status: Disabled

I then attempted to access Facebook again.

Result

Facebook: Reachable

Observation

After disabling the firewall rule, I was able to access and log in to Facebook again. This confirmed that the rule was no longer actively blocking the matching traffic.

Screenshot:
![Ping result](../screenshots/07-after-disabling-the-rule.png)

Step 7 — Main Observations

During the lab, I observed the following:

A domain name can be resolved to an IPv4 address using DNS.

Windows Defender Firewall can create outbound rules based on remote IP addresses.

A firewall rule can block traffic that matches its configured conditions.

Disabling a firewall rule stops that rule from actively blocking matching traffic.

Blocking one IP address does not necessarily block every connection associated with a website.

Large websites can use multiple IP addresses and distributed network infrastructure.

Step 8 — Cybersecurity Concepts Learned
DNS Resolution

DNS, or the Domain Name System, translates human-readable domain names into IP addresses.

Example:

facebook.com → IPv4 address

This allows computers to identify and communicate with network destinations using IP addresses.

IPv4

IPv4 provides numerical addresses used to identify network interfaces or destinations.

Example format:

192.0.2.1

The actual IP address used in this lab was obtained through my own DNS lookup.

Outbound Traffic

Outbound traffic is network traffic leaving my Windows computer. The firewall rule created in this lab controlled outbound traffic destined for a particular remote IP address.

Windows Defender Firewall

Windows Defender Firewall is a host-based firewall that can control network connections using configurable rules.

Firewall rules can use conditions such as:

Program

Protocol

Local IP address

Remote IP address

Local port

Remote port

Network profile

IP-Based Blocking

The firewall rule used in this lab was based on a specific remote IP address. The firewall does not simply block the text facebook.com. Instead, it evaluates network traffic and determines whether that traffic matches the conditions defined by the firewall rule.

Step 9 — IP Blocking vs. Domain Blocking

This lab demonstrated that IP blocking and domain blocking are different concepts.

The basic process can be represented as:

facebook.com
↓
DNS resolution
↓
IP address
↓
Firewall rule
↓
Matching traffic blocked

If the domain resolves to a different IP address, traffic destined for that other address may not match the firewall rule.

Therefore, an IP-based firewall rule should not be considered the same as a rule that directly blocks a domain name.

Step 10 — Limitations
Multiple IP Addresses

A domain can have multiple IP addresses. Therefore, blocking one IP address may not block every connection associated with the website.

Changing DNS Results

DNS results can change over time. A domain may resolve to a different IP address during a later lookup.

Distributed Infrastructure

Large websites often use servers and network infrastructure distributed across multiple locations. Traffic may therefore be directed to different IP addresses.

Shared IP Addresses

An IP address may potentially be associated with more than one service. Blocking an IP address can therefore have unintended effects on other traffic that uses the same address.

IP Blocking Is Not Domain Blocking

The firewall rule created in this lab targeted a specific IP address. It did not create a general rule that understands or blocks every request for the domain facebook.com.

Step 11 — Problems and Challenges

During the lab, I encountered the following challenges:

I initially entered an incorrect IP address and had to verify the address before testing the connection again.

I initially had difficulty navigating the Windows Firewall management interface, but I became more familiar with the available settings after reviewing the rule configuration options.

Step 12 — Final Results
Test Condition	Result
Before blocking	Facebook: Reachable
After enabling firewall rule	Facebook: Unreachable
After disabling firewall rule	Facebook: Reachable

These results showed that the configured outbound firewall rule affected traffic matching the specified remote IP address.

Step 13 — Final Reflection

This lab helped me understand how Windows Defender Firewall can be used to control outbound network traffic. The main lesson I learned is that blocking an IP address is not necessarily the same as blocking an entire website.

Modern websites can use multiple IP addresses and distributed network infrastructure. As a result, blocking a single IP address may only affect some of the traffic associated with a website.

I also learned how DNS resolution connects a human-readable domain name to an IP address and how that IP address can then be used as a condition in a firewall rule.

Overall, the lab provided practical experience with DNS resolution, IPv4 addresses, outbound firewall rules, and IP-based traffic filtering. It also demonstrated the limitations of using a single IP address to control access to a modern website.
