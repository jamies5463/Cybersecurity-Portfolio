**Conducting a security audit of my home network and password management practices**

---

1) **Scope, Method and Goals**

**Scope:** this audit will assess the security of my home network, the password management practices of the two people using the network and the Internet of Things (IoT) devices connected to it. Mitigation recommendations will then be provided to improve security practices within the home.

**Method**:

- Identify best practice for home network, password and IoT security.  
- Log all devices, including IoT devices using the network.  
- Undertake a risk assessment of the three areas against practices, using the router management interface to support information gathering.

**Goals**: The goals for this audit are:

- Produce a controls assessment document.  
- Produce risk mitigation recommendations on improving security across the three areas, and ongoing security maintenance policies and procedures.  
- Implement recommendations and review.


2) **Risk Assessment**

**Asset Inventory and Current Assets**

* End user devices: 2 x smartphones, 1 x personal laptop, 2 x work laptops, 2 x tablets  
* IoT Devices: house alarm, 2 x smart speakers, smart projector  
* Network hardware: router, Wi-Fi extender.  
* Internal network

**Risk Description:** There is currently no systematic management of the network, password or IoT devices. It is likely that current controls do not adhere to the standards recommended by the National Cyber Security Centre (NCSC) and Northern Ireland Cyber Security Centre (NICSC). These two have been chosen as they are both UK-based government cybersecurity agencies: the latter is a regional cybersecurity agency and its advice has been chosen as it provides additional security recommendations beyond those recommended by the NCSC, the UK’s national cybersecurity authority.

**Risk Score:** Risk ratings within this audit were assessed using a simple model based on likelihood and impact.

* **Low Risk**: Existing controls are broadly effective and the likelihood of compromise is limited.  
* **Medium Risk**: Some controls are missing or inconsistently applied, increasing the possibility of compromise or disruption.  
* **High Risk:** Important security controls are absent, creating a significant likelihood of unauthorised access, malware infection, or compromise of credentials.

Using this methodology, the overall pre-mitigation risk rating for the home environment was assessed as **Medium-High**, as several important security controls had either not been implemented or were only partially implemented.

**Additional Comments**: although this audit has been undertaken in a home setting and therefore legal compliance is not a factor in the same way it would be to a private organisation, poor home network and device management nonetheless poses a risk to those in the home and external to it (for example through compromised email accounts, malware  or botnets) and therefore risks to systems and data nonetheless exist in a home environment.

3) **Controls Assessment**

| Home Network Security |  |  |  |
| ----- | :---- | :---- | :---- |
| **Control name** | **Control type and explanation (preventative, detective, deterrent, reactive)** | **Needs to be implemented (Y/N)** | **Priority** |
| Network credentials | Preventative. Network credentials refer to the SSID and password required to join the network itself. Default credentials are considered unsafe as the algorithms used by internet service providers (ISPs) is often public knowledge, and because it is possible that the network details were intercepted. | Y | High |
| Wi-Fi password | Preventative. Ensure that the new password chosen is sufficiently strong. The NCSC recommends either using three random words with no numbers variation in case (owing to difficulty remembering), or using a password manager. The latter is considered more secure owing to the complexity of passwords generated and there being no need to memorise each one. | Y | High |
| Service Set Identifier (SSID \- the name of the Wi-Fi network that a user selected to connect to) | Preventative. Ensure that the ISP is not referenced in the new title of the router. This is intended to prevent a criminal from being able to link a detected network with a specific router. | Y | Medium |
| Encryption standards | Preventative and protective. Wireless networks should be encrypted to either the WPA2 or WPA3 protocol.  | N | Low |
| Firewall | Preventative. The router’s built-in firewall must be switched on. | N | Low |
| Network monitoring | Detective. The network should be checked regularly using the router management interface for unauthorised users and used to remove any unrecognised devices. | Y | High |
| Guest networks | Preventative. A guest Wi-Fi network should be used to separate visitors from trusted home devices. | N | Medium |
| Remote access | Preventative. If the remote access function is not needed, this should be switched off. The remote access function allows the login page for the router management interface to be viewed by all users of the internet, rather than those already connected to your network. This creates a security risk. | N | Low |

| Password Security |  |  |  |
| ----- | :---- | :---- | :---- |
| **Control name** | **Control type and explanation (preventative, detective, deterrent, reactive)** | **Needs to be implemented (Y/N)** | **Priority** |
| Avoid defaults | Preventative. Default passwords are those set by the device manufacturer. Although needed to allow user access to the device for the first time, these should be changed upon setup. These are commonly found on new Wi-Fi routers. | Y | High |
| Password creation | Preventative. Passwords should follow the standards set out by the NCSC, these are using the “three word” password management practices where three unrelated, difficult to guess words are used; or a trusted secure password generator such as those built into commonly used browsers such as Chrome and Edge. **Update:** As of April 2026, the NCSC recommend using passkeys where offered. A passkey is a secure login whereby the user’s device acts as a “key” to their account, and using local authentication on the device such as a fingerprint scanner. | Y | Medium: partially implemented |
| Multi-factor authentication (MFA) | Preventative. Typically used in conjunction with a password, MFA deploys a second layer of authentication such as sending a one-time passcode (OTP) to a user’s device or linked email address. | Y | Medium: partially implemented |

| IoT Devices |  |  |  |
| ----- | :---- | :---- | :---- |
| **Control name** | **Control type and explanation (preventative, detective, deterrent reactive)** | **Needs to be implemented (Y/N)** | **Priority** |
| Network isolation | Preventative. Keep IoT devices on their own separate guest network. This is done in order to prevent infected IoT devices, which as a group are considered less secure, from infecting and spreading to other devices such as laptops and smartphones where system disruption can have greater impact and sensitive data is likely to be stored or transmitted.  | Y | High |
| Default settings | Preventative. Review each device’s security settings after setup. The type of settings depends on the device, however manufacturers often provide information on the role of different security settings on their website/in the device manual. | Y | Medium \- default settings are often designed to balance usability and security, though they should still be reviewed. |
| Factory reset | Preventative. Ensure all devices that are thrown away or sold are factory reset so that data cannot be stolen. | Y | Low \- IoT devices have been thrown away, however this will be done when this happens. |
| Incident response | Reactive. Familiarise yourself with the location of information and support on how to respond to a security incident or device being compromised. Users may wish to keep a tab of bookmarks in their browser of key devices which could pose harm to the system if compromised. | Y | Low \- this has not been done, however typing the name of the device and “device compromised” for all relevant devices shows step-by-step manufacturer guidance on handling breaches. |

   

   

4) **Compliance Score**

Of the 15 measures recommended by the NCSC/NICSC only four have been taken; of the remaining 11, two have been partially undertaken and the remaining nine have not been done at all. In conclusion, compliance is **extremely poor at 27%**, and at the time of the audit if a breach were to occur either through accessing the network or a device on the network there is an increased risk of credential theft, malware infection, unauthorised access or service disruption.

5) **Risk Mitigation Plan**

**Immediate actions**  
*Home network*

* Log into the router using the router management interface and change the login credentials. Similarly to network username and password, these are typically stickered to the router and may have been intercepted by others.  
* Change the SSID using the router management interface. This should be given a name which shows no link to the router manufacturer, model or address. For example “Mr Router”.  
* Change the network password using the router management interface. Routers come with a default password, however these have been known to follow password generation algorithms available on the internet, and are also generally stickered to the router itself meaning others may have gained access to the password in the past.  
* Check encryption standards and change if needed using the router management interface. Encryption standards should be either WPA2 or WPA3, with the latter being preferable but not available on all routers.  
* Check that the firewall is on using the router management interface.  
* Verify the users currently on the network. This is often evident from the device name, however if the name does not indicate the device, an internet MAC address checker can be used.  
* Set up a guest Wi-Fi network using the router management interface. This keeps trusted, regular devices such as those living at the address on a separate network to that given to the guests and IoT devices, reducing the likelihood that guest users and IoT devices can spread malware to devices on the main network.  
* Check remote access settings on the router management interface. This should be disabled if not needed.

*Password management practices*

* Change any default username/password combinations. If users use any username or password that came with a device or account, this should be changed. This is most important with regards to the password.  
* For those using passwords, the NCSC describes a password manager with a strong password itself, typically memorised by the user and/or written down somewhere that it will not be found, as the “gold standard”. The NCSC accepts that users will not always follow the best advice if their technical abilities make this prohibitive, in this instance the organisation recommends combining three random words that the user will remember.   
* For those using passwords, multi-factor authentication (MFA) should be used in conjunction with this. MFA relies on a secondary level of authentication, usually relying on sending an OTP or SMS message to a user’s email address or phone number, respectively.  
* As of April 2026, the NCSC recommends replacing passwords with passkeys. These are now available on user accounts with organisations such as large retailers and video streaming services and are being rolled out. A passkey authenticates the user through their device, rather than a string of characters as in a password. Users add trusted devices, and those devices (such as smartphones) verify the user’s identity locally using methods such as fingerprint scanners.

*IoT Devices*

* Disconnect all IoT devices from the main network and migrate them onto the guest Wi-Fi network.  
* Check the default security settings of each device, and consult the manufacturer’s website/instruction manual on the most secure settings that do not restrict necessary functions. Make adjustments accordingly. For example, some IoT devices have remote access settings which make the login/control page accessible to the internet to allow remote operation. Although useful, if this function is not being used, it should be deactivated to prevent unauthorised access from cybercriminals.  
* Find incident response documentation and store in a known place. For paper manuals this might be one location where all can be found. For those found online, they might be downloaded to one folder or the links to them stored in a tab grouping that can be synced across devices.

**Ongoing actions**  
*Home network*

* Create a “mini audit” checklist of tasks that need performing, along with time frames as to how regularly this must be done. For example “check X every Y months”.  
* Regularly check which users are connected to the network, removing unknown devices as identified. A MAC checker can be used to identify unknown devices.  
* Ensure that the users of the main network know to give guests only the login details for the guest Wi-Fi network.

*Password management practices*

* Ensure passwords for critical services such as the accounts that phones and computers are backed up to and banking apps are changed at a pre-decided frequency. These should follow the password standards set out in the password creation row of the controls assessment.

*IoT devices*

* When IoT devices are sold or thrown away, these should be factory reset to prevent data being stolen from them by cybercriminals.

6) **Implementation and Review**

In summary the implementation of the majority of the controls has been relatively straightforward, with the exception of the network-connected home alarm system. The alarm system comprises numerous devices including a hub, motion sensors and a physical control pad that can be used to arm and disarm it. I did not anticipate the difficulties that failing to disconnect the device from the internet in a planned way prior to changing the Wi-Fi login settings would have. As it is an alarm system, there is a correct method to do this as to not allow would-be criminals seeking to enter the house to gain control over the system. When I changed the network details the software interface was lost and recovery required manual resetting of each device. This required disassembly of each device and a complex process combining both “factory reset” buttons and devices that refused to rejoin the new network or speak with other devices already on it. In future, I would undertake a “pre-planning” operation beforehand to understand what might go wrong and address it beforehand. This experience was however helpful, as it has broadened by technical knowledge by allowing me to understand how factory resetting works, and how this operates with network-connected devices when no user interface is helpful: factory resetting being one of the controls checklist items before disposing of or resetting IoT devices.

The router management interface was relatively simple: I had never logged on before, however the manufacturer-issued login details were on the underside of the router. As discussed, this posed a risk and I changed both username and password immediately after login. The interface was intuitive and the remote access, encryption and firewall settings could be checked easily. Creating a guest Wi-Fi network was also straightforward. All three were in their most secure settings, with one limitation being that WPA2 is the highest standard offered by the router in use. The router does not have the openVPN function, and it was therefore not possible to install a VPN on the router.

In addition to changing the SSID and network password, and the login details for the router management interface, I stored them in a secure password manager that uses biometrics before unlocking. This removes the risk of the network login details being left in the home and being stolen.

No unknown devices were found on the network and some devices did have unusual names that required verification with a MAC address checker, however were not of concern and were the IoT devices mentioned.

As part of my audit I evaluated both mine and my partner’s password management practices. Although I embraced password managers and passkeys on some accounts a while ago, I have no predetermined frequency with which I change my password. Further research suggests that some of my key accounts which would have a large impact in the event of a breach were secured with password and MFA where passkeys are available. My partner’s password management practices were less secure than mine, mostly owing to a combination of unawareness of risk, good practice, and the benefits of passkeys. I explained to my partner the importance of strong passwords, passkeys and MFA, alongside how to set them up. This part of my audit was successful and I have both improved the security of the high risk accounts of myself and my partner, as well as systematised the changing of passwords through the use of a mini-audit checklist, details of which will be outlined below.

In response to this audit I have created a mini-audit checklist. The purpose of this is to systematise the inventorying of key services and websites (for example, banking) and periodically review the security of high-risk accounts and update passwords if compromise is suspected or stronger authentication methods become available . This mini-audit checklist also specifies the frequency with which I check the network for unknown users and check the bookmarked websites I have stored in my browser containing information on how to recover IoT devices in the event of a breach to make sure website links are still valid.

7) **Additional Documentation**

| Mini-Audit Checklist |  |  |  |
| ----- | :---- | :---- | :---- |
| Task | Frequency | Completed (Y/N) | Date and notes |
| Review connected devices on network | Monthly |  |  |
| Remove unrecognised devices | As required |  |  |
| Verify guest Wi-Fi network remains active and separated | Every three months |  |  |
| Review router remote access settings | Every three months |  |  |
| Confirm firewall remains enabled | Every three months |  |  |
| Review router encryption standard (WPA2/WPA3) | Every six months |  |  |
| Review security settings on IoT devices | Every six months |  |  |
| Check incident response bookmarks/links still function | Every six months |  |  |
| Review MFA/passkey status on important accounts | Every six months |  |  |
| Review password manager security and recovery methods | Every six months |  |  |
| Review security of banking/email/cloud backup accounts | Every six months |  |  |
| Factory reset devices before disposal/sale | As required |  |  |
| Review household cybersecurity awareness practices | Annually |  |  |

