# GhostSec Threat Report

**Author**: TheBelfegor
*"I am Belfegor, and your missteps are my demonic pursuit of you"*

PGP Fingerprint: `7E682131E2D23C614C753FB6E07B35ECB25EE5BD`

# Intro

GhostSec first appeared in the 2015, gaining fame primarily for combating ISIS. The group focused on identification, takeover, and blocking of accounts associated with ISIS, also immobilizing websites linked to the organization using DDoS attacks. Over time, the group expanded its attack techniques and targets, as detailed in the subsequent part of the report. GhostSec mainly shifted its focus to attacking Russia, Israel, Cuba, France, Brazil, Nigeria, and the Philippines. As time progressed, the group began targeting an increasing number of countries. As revealed in the later part of the report, their activities went beyond targeting states, as they established their own service for profit.


GhostSec expanded its scope of attacks beyond just DDoS attacks in the mentioned countries. They focused on  OT devices, leveraging exploits on various devices. This group particularly favored the use of the Metasploit tool and utilized it for exploiting SCADA, ICS, and PLC devices, mainly targeting Modbus, Unitronics, and Moxa. In addition to OT, they carried out numerous SQL injection attacks on government related websites of the listed countries.


## Who are the members of GhostSec?
Here are their profiles on the Wire communicator, where they have all their rooms related to the targeted country.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_1.png">
</p>

GhostSec also has other channels, mainly for announcing and showcasing the results of their hacks.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_2.png">
</p>

## Here are a few examples of actions.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_3.png">
</p>

Currently, the group has developed its own ransomware software, which they also sell. One may wonder why the group chose the Python language for creating such malware and why their Command and Control (C2) infrastructure is easily discoverable on Shodan/Censys services.

## GS C2 RANSOMWARE

Shodan Query:
<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_4.png">
</p>

Shodan Hosts List:
<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_5.png">
</p>
                          
Admin Panel:
<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_6.png">
</p>

Affiliate Login:            
<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_7.png">
</p>
                           

## Recon using Maltego

The overall network of connections looks like this; it is quite extensive. The majority of this information consists of malware samples from VirusTotal. Thanks to Maltego, it was possible to gather numerous associated ransomware samples attributed to GhostSec. Additionally, there are mentions of IP addresses linked to C2 servers, connections between members, and their Twitter accounts.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_8.png">
</p>

One of the current samples of **GhostLocker v2**, which has been rewritten in the GOlang version. As observed, the v2 version also connected to the IP address **41.216.183.31**, which is currently inactive, likely indicating that the service has been blocked by the provider.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_9.png">
</p>

The sample named "Anix Private Chair.exe" is the latest sample I managed to obtain. It connects to a C2 with the IP address **41.216.183.31**. In contrast to the initial versions of GhostLocker, which the group guaranteed would be written in C, a brief analysis revealed that this ransomware is written in Python and then converted to C. Unlike its earlier versions, GhostLocker now features a direct chat with the attackers at the address **41.216.183.31/victimchat?id={user id}**.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_10.png">
</p>

The next screenshots will display the remaining found samples of their ransomware.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_11.png">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_12.png">
</p>

The sample in the screenshot connects to a web panel and also performs an upload to **hxxp://195.160.222.36/upload/ghostlocker/**

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_13.png">
</p>

One of the initial versions of GhostLocker written in Python.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_14.png">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_15.png">
</p>

The presented samples are only a part of what has been found. The entire recon conducted using Maltego will be made available for download so that interested individuals can have an overview of all the discovered samples. Moving on to the next part of the recon, you can see the previously mentioned members of the group, including their Twitter accounts and two channels on Telegram.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_16.png">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_17.png">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_18.png">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_19.png">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_20.png">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_21.png">
</p>


It seems that GhostSec has many of its own subdomains.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_22.png">
</p>

 Associated DNS names with ghostsec.net

 <p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_23.png">
</p>

Results from the crt.sh service showing a quite substantial list of subdomains. 

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_24.png">
</p>

One can observe a domain linked with GitLab

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_25.png">
</p>

Interestingly, it is a redirection from an IP **67.205.140.223**

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_26.png">
</p>

Results from searching for this IP on ZoomEye.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_27.png">
</p>

Scanning the IP using VirusTotal indicates that the IP is flagged as malicious

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_28.png">
</p>

Going into details, it indicates that the IP is associated with GitLab.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_29.png">
</p>

Maltego also pointed out correlations in addressing with a GitLab instance.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_30.png">
</p>

I assume that the created and exposed GitLab instance was established as a result of the blocked earlier C2 addresses. I am currently unable to confirm this; the analyzed samples did not indicate it. However, this is a recent change introduced by GhostSec. This service potentially allows them to continue running C2 on their servers by utilizing GitLab. It serves as a clever disguise and complicates correlation.

## What next?

Simple analysis of the ransomware (GhostLocker-python-version) sample with the hash "**898af9ac9850d8901b56a302bdb37ffc**". after execution, the ghostlocker attempts to connect to the IP address **88.218.62.219**.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_31.png">
</p>

The server that the ghostlocker attempted to connect to is located in Russia.
<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_32.png">
</p>

Plaintext 32-byte AES decrypt key. Anyone who captures network traffic can decrypt files because they have the key in plaintext (only for a specific device as the key is generated dynamically). Of course, remembering that this is a POST request. In the logs, only headers and the path are recorded, so what needs to be done is to install your own certificates on the computers and decrypt the traffic at the switch level, for example (something that allows accumulating logs and enables decryption)

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_33.png">
</p>

After execution, the downloaded content remains in the "AppData\Temp" directory in the "onefile" folder.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_34.png">
</p>

Even more amusing is the creators' assertion that this ransomware was written in C. It is misleading, as you can see,  they didn't choose C but opted for Python.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_35.png">
</p>

GhostLocker is a ransomware written in Python and then compiled into C code

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_36.png">
</p>

The folder in which the main files are embedded.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_37.png">
</p>

The question remains why did the creators choose to write ransomware in Python, a language where viruses are known to be slower and easier to analyze? GhostSec, to reduce the detectability of their ransomware, used Nuitka to compile the Python code. The utilization of Nuitka can be observed in screenshots from the IDA program.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_38.png">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_39.png">
</p>

After running the ransomware sample, it presents us with an HTML file containing instructions. Interestingly, GhostSec utilizes a session messenger to communicate with potential victims. It raises the question of why they choose this messenger instead of following the footsteps of other ransomware groups, where direct negotiation often takes place on the onion site of the ransomware.
<br><br>
The decision to use a session messenger may be driven by a variety of factors, including the perceived anonymity and ease of communication it provides. It could also be a strategic choice to distinguish their approach from other ransomware groups.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_40.png">
</p>

GhostLockerV2 Golang version, as it seems, GhostSec is not learning from mistakes and still sends keys in plaintext form to their servers via the POST method.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_41.png">
</p>

This time, it connects to a server located in the Netherlands.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_42.png">
</p>

The program "Detect is Easy" indicates that it is ransomware written in Golang without code obfuscation. I will confirm this in the next screenshots

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_43.png">
</p>

By using IDA, I checked the string names, and as you can see, they are not obfuscated. I consider this a mistake on the part of this group. They create ransomware as a service (RaaS) and distribute files without obfuscation? It's almost like a gift for malware analysts. This allows not only a precise understanding of the sample's operation, such as the execution of the "ghostlocker/encryption.GenerateAESKey" function, but also facilitates the creation of YARA rules for tracking. It's an incredibly kind gesture towards security researchers.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_44.png">
</p>

The file extension change format remains the same compared to the Python version, it is still .ghost

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_45.png">
</p>
  
Ransom note created by GhostLocker V2 looks slightly different than the one presented in their earlier version. In the current version, there are not only visual changes but also a redirection to a chat with GhostSec support.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_46.png">
</p>

Redirection to a chat.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_47.png">
</p>

Negotiation chat looks as follows.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_48.png">
</p>

GhostLocker V2 version allows the attacker to utilize these functions after infecting the machine.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_49.png">
</p>

Referring to what I mentioned earlier while showing the strings of this ransomware using IDA, I mentioned that one can create a YARA rule to hunt down future samples. Here is the created rule, which will also be available for download.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_50.png">
</p>

However, they have not concluded their pursuit of money solely through offering ransomware services. They also derive financial benefits from providing services such as private hacking of selected individuals, doxing, offering DDoS attacks, and many other options.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_51.png">
</p>

The offered webmails can be used for phishing attacks.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_52.png">
</p>

They offer the opportunity to learn OPSEC. They want to teach others something they themselves cannot adhere to.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_53.png">
</p>

They offer TikTok account blocks

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_54.png">
</p>

They also offer the possibility of obtaining data from a person using PayPal or blocking funds held there. They likely have some employee accounts, as such an option is probably reserved for employees and police.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_55.png">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_56.png">
</p>

Concluding this topic, let's move on to a funny mishap and summarize.
<br><br>
Among funny mishaps, it can be noted that one of the individuals (vio) responsible for the onion website lost access to it. Additionally, due to a mishap, the content on the site was replaced, and keys were leaked. 

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_57.png">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/ghostsec/gs_58.png">
</p>

Summing up, the GhostSec group often exaggerates the scope of their operations. Not all of their actions have a significant "destructive" impact. The attacks carried out by this group are typically not highly specialized. In the case of OT devices, they use Metasploit and a custom tool called "killbus" primarily designed to change coil values from 1 to 0, disrupting the proper functioning of PLC controllers. Gaining control involves connecting to open VNC ports, logging into web panels using default credentials, and their attacks on websites, mainly those belonging to "enemy country" often fall within the OWASP Top Ten range. What distinguishes them at first glance is the access to employee accounts and the sale of their capabilities, as outlined above.

# IOC from GhostSec analysis

**URL:**
```
hxxps[:]//195[.]160[.]222[.]36/incrementLaunch
hxxps[:]//41[.]216[.]183[.]31/incrementLaunch
hxxps[:]//195[.]160[.]222[.]36/addInfection
hxxps[:]//195[.]160[.]222[.]36/upload/ghostlocker/lcF1NpUvOFyY0tJ1Y5J9mETf1XbiFLhz
hxxps[:]//88[.]218[.]61[.]141/add
hxxps[:]//88[.]218[.]62[.]219/download
hxxps[:]//195[.]160[.]222[.]36/login?next=%2F
hxxps[:]//94[.]103[.]91[.]246/login?next=/
hxxps[:]//88[.]218[.]61[.]141/incrementLaunches
```

**Hashes:**
```
06202dc1aa8bfeb43dfd52484fc3053dc3a95a076755b1fd08403f19c5f7b490 - SHA256
60e7188170796d26cdedad0698c2ca07aac0f4631713a1c54ecf7c177154f910 - SHA256
4844f44c9de364377f574e4d6a8a77dc0b4d6a67f21ccbf693ac366e52eaa8cb - SHA256
0bc46a38dfe690ccc619c6f9243ea345ac67bb1316029211c344475d7aa4a6d5 - SHA256
abaa2e856434035a0339e1f3cc1c9c7063d96a9f32c6ac25085fc2e87d3ac8b8 - SHA256
5bafabaf5913d6113566f74b8969c6f0250424ec48cd567c687f9db196fbcda5 - SHA256
8c61524a2a8cc77b822a0b9fc7c3eed591cad9a1be8e5425d0475e6c94c251f7 - SHA256
170bd43f183f7ff5f6bb1d1a3226bad5cd7c61f2493acfe57c6f0693c5a37215 - SHA256
0ac094c164d79eafd514eacc0a67f8b74bff24c3df3ba7c88f2908769679867d - SHA256
c9f71fc4f385a4469438ef053e208065431b123e676c17b65d84b6c69ef6748a - SHA256
9b6be74c2c144f8bcb92c8350855d35c14bb7f2b727551c3dd5c8054c4136e3f - SHA256
abac31b5527803a89c941cf24280a9653cdee898a7a338424bd3e9b15d792972 - SHA256
a98f8468d70426ba255469a92d983d653f937d954e936e0ff5d9a0f44f1bdf70 - SHA256
071db35b682bf19a22f2765c6d379cde1c0aa5d243ce44306b4aeddced8e2de9 - SHA256
663ac2d887df18e6da97dd358ebd2bca55404fd4a1c8c1c51215834fc6d11b33 - SHA256
7804e09b2ba224bae06bf23ca2a8b8d668d58b828a8d5aadbbb21c3b7e2acfc4 - SHA256
7d37eddf0b101ff2b633b2ffe33580bdb993a97fecc06874d7b5b07119b9ec99 - SHA256
65d3a922754af96d8d722859ac31f3de96522d50659c67607021f2ac728f9630 - SHA256
0e484560a909fc06b9987db73346efa0ca6750d523f2334913c23e061695f5cc - SHA256
006b067f39f22e14678bfe1f1441bf0c5a62cbcb56b6ef5bd5337aafeb6d937f - SHA256
37214b37345bfbeeacf7b83ecb4e1ce0044acc2066d14e7ef9a87fd56a3b5975 - SHA256
ee227cd0ef308287bc536a3955fd81388a16a0228ac42140e9cf308ae6343a3f - SHA256
```