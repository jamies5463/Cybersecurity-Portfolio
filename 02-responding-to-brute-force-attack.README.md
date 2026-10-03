**Incident Summary and Timeline**  
www\.yummyrecipesforme.com is a cooking recipe hosting website.

See appendix at the bottom of this document for a copy of the tcpdump log.

At 1418 on the 25/07/2026 I was made aware that several visitors to the website had reported issues loading the website. Users reported that after loading, they were prompted to download a file claiming to contain further recipes. After downloading the file, users reported that they were redirected to a further website and that their computers started operating slowly.

The internal team who manage the website initially contacted the third-party website host who was able to temporarily disable the website to prevent the proliferation of malware before passing it on to my team for investigation.

A sandbox environment was created to observe the website behaviour, and the tcpdump Network Protocol Analyser (NPA) was used to investigate the network traffic.

**The tcpdump log timeline is below.**

- The DNS protocol was initiated and requested from dns.google.domain. dns.google is the hostname, and .domain indicates port 53, the port typically used for DNS requests.  
- The host returned the correct IP address for www\.yummyrecipesforme.com, 203.0.113.22.  
- The three-way TCP handshake was initiated and the correct website was loaded using an HTTP GET request.  
- Standard web traffic loading the HTML, CSS and JavaScript content took place.  
- After around two minutes a further DNS request was made for a different website, www\.greatrecipesforme.com and the IP address, 192.0.2.17, was returned.  
- A further three-way TCP handshake took place for this which was successful, and a further HTTP GET request was made for www\.greatrecipesforme.com, the site containing the malware.

**The sandbox testing showed the following:**

- As above, the TCP three-way handshake was successful and the correct website was initially returned.  
- Once loaded the website prompts the user to download a file reportedly containing free recipes. If no action is taken by the user the prompt remains but the download does not execute.  
- Once initiated by the user, the download does two things:  
  * Runs malware on the user’s device, leading to a noticeable impact on performance.  
  * Redirects the user to a different website, www\.greatrecipesforme.com, which is similar in appearance to www\.yummyrecipesforme.com. 

**Analysis**  
The attack used a combination of JavaScript injection and the Hypertext Transfer Protocol (HTTP) protocol to deliver both the malware download prompt, and redirect the user to the illegitimate website. The execution of the file required the user to initiate the download to execute the malware and redirect to the false website, as evidenced in the sandbox testing. This was conceivably done to prevent the user noticing the download running, and may also constitute another attack in itself as it can be exploited to request Sensitive Personally Identifiable Information (SPII) from the victim such as credit card information.

The communications protocol exploited during this attack was HTTP, which sits at the Level 7 Application Layer of the OSI model. Layer 7 can be understood as those network protocols that connect the user to the internet via software or an application. In this scenario, browser software was used to make a Level 7 HTTP request for www\.yummyrecipesforme.com and the same protocol was exploited to request the illegitimate website.

The performance issues experienced by users of the website following the download are indicative of malware, and the Senior Analyst was able to confirm that the attacker gained access to the website admin panel through a brute force attack earlier in the day. This is supported by the identification of the malicious JavaScript script which generated the malware download prompt to the user.

The brute force attack succeeded on the 14th attempt, with the attacker using several related passwords derived from legitimate passwords used within the organisation. Despite 13 failed attempts, no alert was triggered. The investigation also highlighted that the legitimate passwords used by the attacker did not meet the organisation’s password security standards owing to their length and lack of special characters, and that the passwords were variants on the same original password and therefore not unique. These factors enabled the attacker and it is likely that if they were not present the attack could not have taken place, or would have been halted before the attacker gained access to the system.

Initial evidence suggests that the perpetrator of the attack may be an ex-employee who recently worked for the organisation: this working conclusion has been made on the basis of a publicly stated grudge that the individual holds against the organisation, and that the individual in question had routine access to the necessary passwords to be able to access the admin panel of the website during the period of employment.

**Actions and Recommendations**  
**Actions**

- tcpdump analysis was undertaken to understand the network activity and protocols used. This was supplemented with running the website in a sandbox to better understand the operation of the website and malware  
- The third-party website host was contacted to disable the website as a temporary measure to prevent the proliferation of the malware.  
- The team responsible for managing the website was able to reset the password of the admin panel, regaining access and preventing the attacker from staging a further attack..  
- A Senior Analyst was made aware and undertook their own investigation, confirming a brute force attack, changes made to website’s JavaScript code, the behaviour of the malware, and the insertion of a script redirecting users to an illegitimate website.  
- The website was restored to a clean version from before the attack, removing the known malware and clearing any other unwanted changes to the code which may have been inserted. This allowed for the website to be restored.  
- An emergency-audit of all passwords and critical system information that the former employee suspected of undertaking the attack was held, and the relevant login credentials for systems identified were immediately changed.

**Recommendations**  
The attack highlighted a lack of defensive measures against brute force attacks, and weaknesses in user authentication. This report recommends the following security measures:

- **Clear and enforceable passwords policies.** CISA recommends that where passwords are used they should be at least 16 characters long, contain either random figures that are not similar to other passwords or a unique memorable phrase of 4-7 words (CISA, No Date). Password complexity requirements must also be enforceable, preventing users from entering passwords which do not meet the standard.  
- **Multi-factor authentication (MFA)**. MFA is recommended as an additional measure to supplement strong password protection, typically requiring a legitimate employee to provide a second level of authentication such as a prompt to their phone.  
- **Web Application Firewall (WAF) configuration settings review**. The organisation already makes use of a WAF, but despite this the brute force attack was not detected. This suggests a configuration issue, as the software used by the organisation is considered an effective tool.  
- **Brute force attack alerts**. No alert system presently exists, the implementation of such a system would ensure that key individuals and teams are alerted who can take action.  
- **Automated actions**: system configuration settings can also be set to lock systems after a certain number of failed login attempts as well as employing measures such as rate limiting which will only allow users to perform an action a certain number of times within a fixed period of time.

**Bibliography**  
CISA (No Date) https\://www\.cisa.gov/secure-our-world/use-strong-passwords

**Appendix: tcpdump log**

*14:18:32.192571 IP 192.168.1.42.52444 \> dns.google.domain: 35084+ A? yummyrecipesforme.com. (24)*

*14:18:32.204388 IP dns.google.domain \> 192.168.1.42.52444: 35084 1/0/0 A 203.0.113.22 (40)* 

*14:18:36.786501 IP 192.168.1.42.36086 \> yummyrecipesforme.com.http: Flags \[S\], seq 2873951608, win 65495, options \[mss 65495,sackOK,TS val 3302576859 ecr 0,nop,wscale 7\], length 0*

*14:18:36.786517 IP yummyrecipesforme.com.http \> 192.168.1.42.36086: Flags \[S.\], seq 3984334959, ack 2873951609, win 65483, options \[mss 65495,sackOK,TS val 3302576859 ecr 3302576859,nop,wscale 7\], length 0*

*14:18:36.786529 IP 192.168.1.42.36086 \> yummyrecipesforme.com.http: Flags \[.\], ack 1, win 512, options \[nop,nop,TS val 3302576859 ecr 3302576859\], length 0*

*14:18:36.786589 IP 192.168.1.42.36086 \> yummyrecipesforme.com.http: Flags \[P.\], seq 1:74, ack 1, win 512, options \[nop,nop,TS val 3302576859 ecr 3302576859\], length 73: HTTP: GET / HTTP/1.1*

*14:18:36.786595 IP yummyrecipesforme.com.http \> 192.168.1.42.36086: Flags \[.\], ack 74, win 512, options \[nop,nop,TS val 3302576859 ecr 3302576859\], length 0 …\<a lot of traffic on the port 80\>*

*14:20:32.192571 IP 192.168.1.42.52444 \> dns.google.domain: 21899+ A? greatrecipesforme.com. (24)*

*14:20:32.204388 IP dns.google.domain \> 192.168.1.42.52444: 21899 1/0/0 A 192.0.2.17 (40)* 

*14:25:29.576493 IP 192.168.1.42.56378 \> greatrecipesforme.com.http: Flags \[S\], seq 1020702883, win 65495, options \[mss 65495,sackOK,TS val 3302989649 ecr 0,nop,wscale 7\], length 0* 

*14:25:29.576510 IP greatrecipesforme.com.http \> 192.168.1.42.56378: Flags \[S.\], seq 1993648018, ack 1020702884, win 65483, options \[mss 65495,sackOK,TS val 3302989649 ecr 3302989649,nop,wscale 7\], length 0*

*14:25:29.576524 IP 192.168.1.42.56378 \> greatrecipesforme.com.http: Flags \[.\], ack 1, win 512, options \[nop,nop,TS val 3302989649 ecr 3302989649\], length 0*

*14:25:29.576590 IP 192.168.1.42.56378 \> greatrecipesforme.com.http: Flags \[P.\], seq 1:74, ack 1, win 512, options \[nop,nop,TS val 3302989649 ecr 3302989649\], length 73: HTTP: GET / HTTP/1.1* 

*14:25:29.576597 IP greatrecipesforme.com.http \> 192.168.1.42.56378: Flags \[.\], ack 74, win 512, options \[nop,nop,TS val 3302989649 ecr 3302989649\], length 0 …\<a lot of traffic on the port 80\>...* 

