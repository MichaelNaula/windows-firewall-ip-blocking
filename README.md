# windows-firewall-ip-blocking
Windows Firewall lab demonstrating IP-based website blocking
**Project Overview**
This project demonstrates how to use Windows Defender Firewall with Advanced Security to create an outbound firewall rule that blocks network traffic to a specific IPv4 address.
For this lab, I used Facebook (facebook.com) as the example website. I first resolved the website's domain name to an IP address using ping and nslookup. I then created a Windows Firewall outbound rule to block traffic to the selected IP address. Finally, I tested the website before blocking, after enabling the firewall rule, and after disabling the rule.
The purpose of this project is to understand how IP-based firewall blocking works and why blocking an IP address is not necessarily the same as blocking an entire website.

**Objectives**
The objectives of this lab were to:
•	Resolve a website domain name to an IPv4 address.
•	Understand Domain Name System (DNS) resolution.
•	Identify an IPv4 address associated with a website.
•	Create an outbound Windows Firewall rule.
•	Block traffic to a specific remote IP address.
•	Test network connectivity before and after blocking.
•	Disable the firewall rule and test connectivity again.
•	Understand the limitations of IP-based website blocking.
•	Understand why large websites may use multiple IP addresses and distributed infrastructure such as CDNs.

**Lab Environment**
•	Operating System: Windows
•	Firewall: Windows Defender Firewall with Advanced Security
•	Target Website: Facebook (facebook.com)
•	Firewall Direction: Outbound
•	Rule Type: IP-based blocking

**1. DNS Resolution and Finding the IP Address**
The first step was to determine which IP address was associated with facebook.com.
I used Windows Command Prompt and ran: ping facebook.com
I also used: nslookup facebook.com
DNS, (Domain Name System), translates human-readable domain names such as facebook.com into IP addresses that computers can use to communicate across a network.
The IPv4 address returned during the lookup was used as the remote IP address for the Windows Firewall rule.
Screenshot 1a— IP Address Resolution Using Ping
 ![Ping result](../screenshots/01a-ip-address-ping.png)
The screenshot shows the domain name and the IPv4 address returned by the ping command.
Screenshot 1b— IP Address Resolution Using nslookup
 ![Ping result](../screenshots/01b-ip-address-nslookup.png)
The screenshot shows the DNS lookup information returned by nslookup.

**2. Testing the Website Before Blocking**
Before creating the firewall rule, I tested whether Facebook was reachable from my Windows computer.
I opened: https://www.facebook.com
The purpose of this step was to establish a baseline. This allowed me to compare the website's behavior before and after the firewall rule was enabled.
Screenshot 2— Facebook Before Blocking
 ![Ping result](../screenshots/02-before-blocking.png)
This screenshot provides evidence that Facebook was reachable before the firewall rule was enabled.

**3. Creating the Windows Firewall Outbound Rule**
I opened Windows Defender Firewall with Advanced Security by running: wf.msc
Screenshot 3— Opening Windows Defender Firewall with Advanced Security
 ![Ping result](../screenshots/03-opening-windows-firewall-with-advanced-security.png)
I then navigated to:
Outbound Rules --> New Rule 
I created a custom outbound rule and specified the IPv4 address obtained during the DNS resolution step.
The rule was configured to apply to outbound traffic destined for the selected remote IP address.
Screenshot 4— Firewall Rule Creation
 ![Ping result](../screenshots/04-Block-Facebook-IP.png)
This screenshot shows the configuration of the outbound firewall rule.

**4. Configuring the Rule to Block the Connection**
The firewall rule was configured with the action: Block the connection
This means Windows Firewall should prevent network traffic matching the rule from reaching the specified remote IP address.
Screenshot 5— Rule Properties
 ![Ping result](../screenshots/05-rule-properties.png)
This screenshot provides evidence that the firewall rule was configured to Block the connection.

**5. Testing After Enabling the Firewall Rule**
After creating and enabling the firewall rule, I attempted to access Facebook again. The purpose of this test was to determine whether blocking the selected IP address affected access to the website.
Test Result
After enabling the firewall rule, I attempted to access Facebook again. The website was blocked. This result demonstrated that blocking the selected IP address affected access to Facebook during this test.
However, blocking one IP address does not necessarily guarantee that an entire website will always be inaccessible. Large websites can use multiple IP addresses and distributed network infrastructure.
Screenshot 6— Website After Blocking
 ![Ping result](../screenshots/06-after-blocking.png)
This screenshot provides evidence of the website's behavior after the firewall rule was enabled.

**6. Disabling the Firewall Rule**
After completing the blocking test, I disabled the firewall rule instead of deleting it. This allowed me to preserve the configuration while stopping the rule from actively blocking the matching traffic.
I then tested access to Facebook again.
Screenshot 7— Website After Disabling the Rule
![Ping result](../screenshots/07-after-disabling-the-rule.png)
This screenshot provides evidence of the website's behavior after the firewall rule was disabled.

**7. What I Learned**
**DNS Resolution**
DNS stands for Domain Name System. It allows users to access websites using domain names instead of having to remember numerical IP addresses.
For example: facebook.com --> IPv4 address
When I used ping or nslookup, my computer performed DNS resolution to determine an IP address associated with the domain.
DNS resolution is important because network communication uses IP addresses to identify network endpoints.
**IPv4 Addresses**
An IPv4 address is a numerical address used to identify a network interface or endpoint using the IPv4 protocol. An IPv4 address has four numerical sections separated by periods.
For example: 192.0.2.1
The actual IP address used in this lab was obtained from my own DNS lookup.
**Outbound Network Traffic**
Outbound traffic is network traffic leaving my computer. Windows Defender Firewall can apply rules to outbound connections. In this lab, I created an outbound rule that matched traffic destined for a particular remote IP address. This demonstrates how a firewall can control communication between a computer and external network destinations.
**Windows Defender Firewall**
Windows Defender Firewall is a host-based firewall included with Windows.

It can use rules to allow or block network connections based on characteristics such as:
•	Program
•	Protocol
•	Local port
•	Remote port
•	Local IP address
•	Remote IP address
•	Network profile
In this project, I used a remote IP address as the primary condition for the blocking rule.
Firewall Rules
A firewall rule defines how the firewall should handle network traffic that matches specified conditions. The rule created during this lab was an outbound blocking rule.
The basic concept was:
My windows computer-->Outbound traffic<--Specified remote IPv4 address--X Firewall blocks

When the rule was disabled, Windows Firewall no longer applied that blocking rule to the matching traffic.

**8. IP Blocking vs. Domain Blocking**
One of the most important lessons from this project is that blocking an IP address is not the same as blocking a domain name. The firewall rule created in this lab targeted an IP address, not the text facebook.com.
The process can be represented as:
facebook.com --> DNS resolution--> IP address--> Firewall rule--> Block traffic

The firewall is therefore blocking traffic to the selected IP address. It is not necessarily blocking every IP address that could be associated with facebook.com.

9. **Multiple IP Addresses and CDNs**
Large websites such as Facebook use large-scale distributed network infrastructure. A domain can be associated with multiple IP addresses, and the IP address returned by DNS can vary depending on factors such as location, DNS resolver, network configuration, and the website's infrastructure.
Large websites also commonly use distributed systems and Content Delivery Networks (CDNs) or similar infrastructure to improve performance, availability, and scalability.
Because of this, blocking one IP address may not completely block access to a website.
For example:
                 facebook.com
                      |
             +--------+--------+
             |        |        |
             v        v        v
            IP A     IP B     IP C
             |        |        |
             X        ✓        ✓
          blocked   allowed  allowed
If only IP A is blocked, connections using IP B or IP C may still succeed.

**10. Limitations of IP-Based Blocking**
This lab demonstrated several limitations of IP-based blocking.
1. A domain can have multiple IP addresses
Blocking one address does not necessarily block all addresses associated with the domain.
2. DNS results can change
The IP address returned for a domain can change over time.
Therefore, a firewall rule based on one IP address may become ineffective if the website begins using another address.
3. Shared Infrastructure
Multiple services or websites can potentially use the same network infrastructure or IP addresses.
Blocking an IP address can therefore have unintended effects if other services use the same address.
4. Large Websites Use Distributed Infrastructure
Modern websites can operate across many servers and locations. Blocking a single address is therefore not always an effective way to block an entire service.
5. IP Blocking Is Different From Domain Filtering
A simple IP-based firewall rule does not inherently understand that an IP address represents a particular domain.
It simply matches network traffic against the conditions specified in the firewall rule.
**11. Conclusion**
This project demonstrated how Windows Defender Firewall can be used to create an outbound rule that blocks traffic to a specific IPv4 address.
During this lab, I learned how to:
•	Use ping and nslookup to perform DNS resolution.
•	Identify an IPv4 address associated with a domain.
•	Create an outbound Windows Firewall rule.
•	Configure a firewall rule to block a remote IP address.
•	Test network connectivity before and after applying the rule.
•	Disable the firewall rule and test connectivity again.
•	Understand the difference between IP-based blocking and domain-based blocking.
The most important lesson is that blocking an IP address does not necessarily mean blocking an entire website. Modern websites can use multiple IP addresses, distributed infrastructure, and CDNs. As a result, IP-based blocking can be incomplete and may not be a reliable method for blocking an entire website.
This lab provided a practical introduction to Windows Firewall configuration and demonstrated an important concept in network security: the effectiveness of a firewall rule depends on exactly what traffic the rule matches and how the destination service is structured.

**12. Project Structure**
The final project is organized as follows:
windows-firewall-ip-blocking/
│
├── README.md
│
├── screenshots/
│   ├── 01a-ip-address-ping.png
│   ├── 01b-ip-address-nslookup.png
│   ├── 02-opening-windows-firewall-with-advanced-security.png
│   ├── 03-before-blocking.png
|   ├── 04-Block-Facebook-IP.png
│   ├── 05-rule-properties.png
│   ├── 06-after-blocking.png
│   └── 07-after-disabling-the-rule.png
│
└── notes/
    └── lab-notes.md
**Evidence**
The screenshots in this repository provide visual evidence of the main stages of the lab, including:
•	IP address resolution using ping
•	DNS resolution using nslookup
•	Website testing before blocking
•	Firewall rule creation
•	Firewall rule properties
•	Website testing after blocking
•	Website testing after disabling the rule

