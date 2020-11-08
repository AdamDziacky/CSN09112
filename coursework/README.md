<img src="https://github.com/billbuchanan/csn09112/blob/master/zadditional/top_csn09112.png"/>

# CSN09112 - Network Security and Cryptography
<p align="right">Bill Buchanan, Rich Macfarlane</p>

## Running the bot and controller
You can download the Bot onto the Ubuntu machine using:

<pre>
wget http://networksims.com/Archive.zip
unzip Archive.zip
</pre>
<p>Note: Current version is 3.5a</p>
<p>Go to your Windows machine on the DMZ, and download the ZIP file (Archive.zip). Otherwise download the controller to the Kali machine on the DMZ, and run:</p>

<pre>
mono controller.exe
</pre>

Take a note of the IP address of the controller (W.X.Y.Z). Now got your Ubuntu machine, and run:</p>

<pre>
mono bot.exe W.X.Y.Z
</pre>

The bot and the controller should connect to each other.

## Outline Requirements

Botnets are a particular problem, where bot agents may infect machines inside an organisation’s network and connect back to a botnet controller out on the Internet, to receive commands and undertake malicious activities. The focus of this coursework is to create a virtualized testbed environment to analyse a particular botnet agent and the communications to its controller, to create and test a detection system to detect its activities, and then to mitigate its use in future with some firewall based defences.

* Configure a working perimeter network topology with a firewall, DMZ, and host systems as a testbed for the coursework. Secure the VMs by changing login passwords.
* Analyse the operation of the running Bot agent and Botnet controller, including any network scanning by the bot, activity on the host, network connections created, and any communications between the bot and controller.
* Create and test a detection system for the Botnet agent and controller using an IDS sensor.
* Create a closed perimeter, firewall policy configuration to prevent future communications for this particular botnet, but allow certain valid traffic, specified in next section.

Your network architecture similar to that shown in Figure 1 should be created with the VMs provided using two private address spaces, which you will be assigned on Moodle specifically for the coursework. The Bot agent should be run from the internal trusted Private network.

Start by allowing all traffic from the internal network out to the external network so the bot can communicate with the bot controller. Then use this architecture as your testbed to thoroughly investigate and analyse the Botnet activity. Try to plan and be scientific in the experimental method you use and don’t simply run it once and report. Static analysis can then be used to compliment the dynamic analysis. 
After this, design an Intrusion Detection System (IDS) which will detect the various bot activities, leading to an implementation of a prototype using a Snort sensor running on the internal Linux system. The alerts generated should be useful to a security admin. If you have time investigate tuning the rules.
Once the IDS has been tested, design and create firewall rules to close down the firewall to prevent future botnet activity, possibly highlight/log specific botnet activity, and test the configuration. Create a basic perimeter firewall solution, based around the current topology to provide a public web server from the external network, and Internet access from the internal network.

![Figure 1](https://github.com/billbuchanan/csn09112/blob/master/coursework/cw01.png?raw=true)

## Demo

The following provides an overview of the task [here](https://www.youtube.com/watch?v=94iEY0XxPM8).

Snort should be installed within Ubuntu, and is run with:
<pre>
snort -c 1.rules -i eth0 -l log
</pre>

When you are running the botnet, first note the IP address of the controller, and then run it:
<pre>
mono bot.exe
</pre>

A sample rules file has been placed in the instance. A good method of analysis is to get the PCAP fo the communication and then use Snort in an offline mode.

## Marking schedule

The coursework should be submitted via Turnitin (submit.ac.uk), in a PDF format, if possible. The hand-in date is 11:55pm on 18 Decemember 2019. It will be marked as follows:

**Research [20 marks]**

A brief literature review towards your botnet analysis method and IDS rule development, demonstrating an understanding of the topics and using research from a variety of quality sources (cited in the text). Try to include some critical analysis - for example strengths and weaknesses, justification, and highlighting findings which inform the later work - and possibly recent examples and how they were analysed.
<p align="right">[20 marks]</p>

**Botnet Analysis [40 marks]**

Configure a working perimeter network topology with a firewall, DMZ, and host systems as a testbed for the coursework. For example annotated network diagram, and some basic configuration/connectivity testing shown and discussed briefly.
Discuss methods informed from the research, and aply these to analyse the operation of the running Bot agent and Botnet controller, including any connections created by the bot, possible host activities on the victim, communications between the bot and controller, and anyother bot behaviour. For example screen shots and brief discussion for: botnet components running, analysis tools, outputs and interesting data, tools and outputs of cracking codes, with brief discussion.
- Dynamic analysis of bot and botnet controller could include identifying botnet network connections and traffic, filtering out unrelated traffic using appropriate tools, identify types of traffic generated, identify specific botnet commands and responses, decoing botnet traffic if necessary. Challenge: create your own bot traffic so individual command can be sent and analysed separately. 
- Static Analysis Challenge: To verify your findings from the dynamic analysis of the botnet behavior, try to reverse engineer the bot agent code and statically analyse the code.
<p align="right">[40 marks]</p>

**Prototype Defenses Implementation and Testing [30 marks]**

Apply method from the research, which should define an outline prototype implementation of the defences.
- From your botnet analysis, create and test a basic prototype detection system for the Botnet agent and controller using an IDS sensor. Create IDS rules/signatures to detect the bot activity and not excessive many false positives. This section could show the Snort rules with descriptions of how they work, and screen shots of the testing/outputs and discussion on this.
- Create a closed perimeter firewall configuration to prevent/highlight future communications for this particular botnet, but allow certain valid traffic (specified in requirements spec’). Again show the configuration/rules and testing using screen shot snippets with brief explanation, and any discussion on the findings/outputs.
<p align="right">[30 marks]</p>

**References/Presentation [10 marks]**

The academic report should be written in a formal style, in 3rd person, and well presented.
Full academic referencing of peer reviewed papers, technical papers, books, and web sites, using thorough the Harvard referencing format.
- Reference all materials used, citing every reference in the body of the report.
- All references cited should be listed at the end of the report, using Harvard referencing format.
<p align="right">[10 marks]</p>

The report should use the Harvard format for all of the references, and, if possible, should include EVERY reference to material sourced from other places. Also, the report should be up to 20 pages long (where appendices do not count in the page count number). 

## Network stetup
You can use any two network address ranges for your network. If you know your group number, you can use the following:

### Allocation A

<pre>
Allocated	Ubuntu	        	Windows	        Em0	    Em1 (Private)	    Em2 (DMZ)
----------------------------------------------------------------------------------------
Group_001	192.168.1.7/24		192.168.2.7/24	DHCP	192.168.1.254/24	192.168.2.254/24
Group_002	192.168.3.7/24		192.168.4.7/24	DHCP	192.168.3.254/24	192.168.4.254/24
Group_003	192.168.5.7/24		192.168.6.7/24	DHCP	192.168.5.254/24	192.168.6.254/24
Group_004	192.168.7.7/24		192.168.8.7/24	DHCP	192.168.7.254/24	192.168.8.254/24
Group_005	192.168.9.7/24		192.168.10.7/24	DHCP	192.168.9.254/24	192.168.10.254/24
Group_006	192.168.11.7/24		192.168.12.7/24	DHCP	192.168.11.254/24	192.168.12.254/24
Group_007	192.168.13.7/24		192.168.14.7/24	DHCP	192.168.13.254/24	192.168.14.254/24
Group_008	192.168.15.7/24		192.168.16.7/24	DHCP	192.168.15.254/24	192.168.16.254/24
Group_009	192.168.17.7/24		192.168.18.7/24	DHCP	192.168.17.254/24	192.168.18.254/24
Group_010	192.168.19.7/24		192.168.20.7/24	DHCP	192.168.19.254/24	192.168.20.254/24
Group_011	192.168.21.7/24		192.168.22.7/24	DHCP	192.168.21.254/24	192.168.22.254/24
Group_012	192.168.23.7/24		192.168.24.7/24	DHCP	192.168.23.254/24	192.168.24.254/24
Group_013	192.168.25.7/24		192.168.26.7/24	DHCP	192.168.25.254/24	192.168.26.254/24
Group_014	192.168.27.7/24		192.168.28.7/24	DHCP	192.168.27.254/24	192.168.28.254/24
Group_015	192.168.29.7/24		192.168.30.7/24	DHCP	192.168.29.254/24	192.168.30.254/24
Group_016	192.168.31.7/24		192.168.32.7/24	DHCP	192.168.31.254/24	192.168.32.254/24
Group_017	192.168.33.7/24		192.168.34.7/24	DHCP	192.168.33.254/24	192.168.34.254/24
Group_018	192.168.35.7/24		192.168.36.7/24	DHCP	192.168.35.254/24	192.168.36.254/24
Group_019	192.168.37.7/24		192.168.38.7/24	DHCP	192.168.37.254/24	192.168.38.254/24
Group_020	192.168.39.7/24		192.168.40.7/24	DHCP	192.168.39.254/24	192.168.40.254/24
Group_021	192.168.41.7/24		192.168.42.7/24	DHCP	192.168.41.254/24	192.168.42.254/24
Group_022	192.168.43.7/24		192.168.44.7/24	DHCP	192.168.43.254/24	192.168.44.254/24
Group_023	192.168.45.7/24		192.168.46.7/24	DHCP	192.168.45.254/24	192.168.46.254/24
Group_024	192.168.47.7/24		192.168.48.7/24	DHCP	192.168.47.254/24	192.168.48.254/24
Group_025	192.168.49.7/24		192.168.50.7/24	DHCP	192.168.49.254/24	192.168.50.254/24
Group_026	192.168.51.7/24		192.168.52.7/24	DHCP	192.168.51.254/24	192.168.52.254/24
Group_027	192.168.53.7/24		192.168.54.7/24	DHCP	192.168.53.254/24	192.168.54.254/24
Group_028	192.168.55.7/24		192.168.56.7/24	DHCP	192.168.55.254/24	192.168.56.254/24
Group_029	192.168.57.7/24		192.168.58.7/24	DHCP	192.168.57.254/24	192.168.58.254/24
Group_030	192.168.59.7/24		192.168.60.7/24	DHCP	192.168.59.254/24	192.168.60.254/24
Group_031	192.168.61.7/24		192.168.62.7/24	DHCP	192.168.61.254/24	192.168.62.254/24
Group_032	192.168.63.7/24		192.168.64.7/24	DHCP	192.168.63.254/24	192.168.64.254/24
Group_033	192.168.65.7/24		192.168.66.7/24	DHCP	192.168.65.254/24	192.168.66.254/24
Group_034	192.168.67.7/24		192.168.68.7/24	DHCP	192.168.67.254/24	192.168.68.254/24
Group_035	192.168.69.7/24		192.168.70.7/24	DHCP	192.168.69.254/24	192.168.70.254/24
Group_036	192.168.71.7/24		192.168.72.7/24	DHCP	192.168.71.254/24	192.168.72.254/24
Group_037	192.168.73.7/24		192.168.74.7/24	DHCP	192.168.73.254/24	192.168.74.254/24
Group_038	192.168.75.7/24		192.168.76.7/24	DHCP	192.168.75.254/24	192.168.76.254/24
Group_039	192.168.77.7/24		192.168.78.7/24	DHCP	192.168.77.254/24	192.168.78.254/24
Group_040	192.168.79.7/24		192.168.80.7/24	DHCP	192.168.79.254/24	192.168.80.254/24
Group_041	192.168.81.7/24		192.168.82.7/24	DHCP	192.168.81.254/24	192.168.82.254/24
Group_042	192.168.83.7/24		192.168.84.7/24	DHCP	192.168.83.254/24	192.168.84.254/24
Group_043	192.168.85.7/24		192.168.86.7/24	DHCP	192.168.85.254/24	192.168.86.254/24
Group_044	192.168.87.7/24		192.168.88.7/24	DHCP	192.168.87.254/24	192.168.88.254/24
Group_045	192.168.89.7/24		192.168.90.7/24	DHCP	192.168.89.254/24	192.168.90.254/24
Group_046	192.168.91.7/24		192.168.92.7/24	DHCP	192.168.91.254/24	192.168.92.254/24
Group_047	192.168.93.7/24		192.168.94.7/24	DHCP	192.168.93.254/24	192.168.94.254/24
Group_048	192.168.95.7/24		192.168.96.7/24	DHCP	192.168.95.254/24	192.168.96.254/24
Group_049	192.168.97.7/24		192.168.98.7/24	DHCP	192.168.97.254/24	192.168.98.254/24
Group_050	192.168.99.7/24		192.168.100.7/24 DHCP	192.168.99.254/24	192.168.100.254/24
Group_051	192.168.101.7/24	192.168.102.7/24 DHCP	192.168.101.254/24	192.168.102.254/24
Group_052	192.168.103.7/24	192.168.104.7/24 DHCP	192.168.103.254/24	192.168.104.254/24
Group_053	192.168.105.7/24	192.168.106.7/24 DHCP	192.168.105.254/24	192.168.106.254/24
Group_054	192.168.107.7/24	192.168.108.7/24 DHCP	192.168.107.254/24	192.168.108.254/24
Group_055	192.168.109.7/24	192.168.110.7/24 DHCP	192.168.109.254/24	192.168.110.254/24
Group_056	192.168.111.7/24	192.168.112.7/24 DHCP	192.168.111.254/24	192.168.112.254/24
Group_057	192.168.113.7/24	192.168.114.7/24 DHCP	192.168.113.254/24	192.168.114.254/24
Group_058	192.168.115.7/24	192.168.116.7/24 DHCP	192.168.115.254/24	192.168.116.254/24
Group_059	192.168.117.7/24	192.168.118.7/24 DHCP	192.168.117.254/24	192.168.118.254/24
Group_060	192.168.119.7/24	192.168.120.7/24 DHCP	192.168.119.254/24	192.168.120.254/24
Group_061	192.168.121.7/24	192.168.122.7/24 DHCP	192.168.121.254/24	192.168.122.254/24
Group_062	192.168.123.7/24	192.168.124.7/24 DHCP	192.168.123.254/24	192.168.124.254/24
Group_063	192.168.125.7/24	192.168.126.7/24 DHCP	192.168.125.254/24	192.168.126.254/24
Group_064	192.168.127.7/24	192.168.128.7/24 DHCP	192.168.127.254/24	192.168.128.254/24
Group_065	192.168.129.7/24	192.168.130.7/24 DHCP	192.168.129.254/24	192.168.130.254/24
Group_066	192.168.131.7/24	192.168.132.7/24 DHCP	192.168.131.254/24	192.168.132.254/24
Group_067	192.168.133.7/24	192.168.134.7/24 DHCP	192.168.133.254/24	192.168.134.254/24
Group_068	192.168.135.7/24	192.168.136.7/24 DHCP	192.168.135.254/24	192.168.136.254/24
Group_069	192.168.137.7/24	192.168.138.7/24 DHCP	192.168.137.254/24	192.168.138.254/24
Group_070	192.168.139.7/24	192.168.140.7/24 DHCP	192.168.139.254/24	192.168.140.254/24
Group_071	192.168.141.7/24	192.168.142.7/24 DHCP	192.168.141.254/24	192.168.142.254/24
Group_072	192.168.143.7/24	192.168.144.7/24 DHCP	192.168.143.254/24	192.168.144.254/24
Group_073	192.168.145.7/24	192.168.146.7/24 DHCP	192.168.145.254/24	192.168.146.254/24
Group_074	192.168.147.7/24	192.168.148.7/24 DHCP	192.168.147.254/24	192.168.148.254/24
Group_075	192.168.149.7/24	192.168.150.7/24 DHCP	192.168.149.254/24	192.168.150.254/24
Group_075	192.168.151.7/24	192.168.152.7/24 DHCP	192.168.151.254/24	192.168.152.254/24
Group_077	192.168.153.7/24	192.168.154.7/24 DHCP	192.168.153.254/24	192.168.154.254/24
Group_078	192.168.155.7/24	192.168.156.7/24 DHCP	192.168.155.254/24	192.168.156.254/24
Group_079	192.168.157.7/24	192.168.158.7/24 DHCP	192.168.157.254/24	192.168.158.254/24
Group_080	192.168.159.7/24	192.168.160.7/24 DHCP	192.168.159.254/24	192.168.160.254/24
Group_081	192.168.161.7/24	192.168.162.7/24 DHCP	192.168.161.254/24	192.168.162.254/24
Group_082	192.168.163.7/24	192.168.164.7/24 DHCP	192.168.163.254/24	192.168.164.254/24
Group_083	192.168.165.7/24	192.168.166.7/24 DHCP	192.168.165.254/24	192.168.166.254/24
Group_084	192.168.167.7/24	192.168.168.7/24 DHCP	192.168.167.254/24	192.168.168.254/24
Group_085	192.168.169.7/24	192.168.170.7/24 DHCP	192.168.169.254/24	192.168.170.254/24
Group_086	192.168.171.7/24	192.168.172.7/24 DHCP	192.168.171.254/24	192.168.172.254/24
Group_087	192.168.173.7/24	192.168.174.7/24 DHCP	192.168.173.254/24	192.168.174.254/24
</pre>

### Allocation B

<pre>
Allocated	Ubuntu	        Windows	        Em0	    Em1 (Private)	    Em2 (DMZ)
----------------------------------------------------------------------------------------
Group_001	172.16.1.7/24		172.16.2.7/24	DHCP	172.16.1.254/24	172.16.2.254/24
Group_002	172.16.3.7/24		172.16.4.7/24	DHCP	172.16.3.254/24	172.16.4.254/24
Group_003	172.16.5.7/24		172.16.6.7/24	DHCP	172.16.5.254/24	172.16.6.254/24
Group_004	172.16.7.7/24		172.16.8.7/24	DHCP	172.16.7.254/24	172.16.8.254/24
Group_005	172.16.9.7/24		172.16.10.7/24	DHCP	172.16.9.254/24	172.16.10.254/24
Group_006	172.16.11.7/24		172.16.12.7/24	DHCP	172.16.11.254/24	172.16.12.254/24
Group_007	172.16.13.7/24		172.16.14.7/24	DHCP	172.16.13.254/24	172.16.14.254/24
Group_008	172.16.15.7/24		172.16.16.7/24	DHCP	172.16.15.254/24	172.16.16.254/24
Group_009	172.16.17.7/24		172.16.18.7/24	DHCP	172.16.17.254/24	172.16.18.254/24
Group_010	172.16.19.7/24		172.16.20.7/24	DHCP	172.16.19.254/24	172.16.20.254/24
Group_011	172.16.21.7/24		172.16.22.7/24	DHCP	172.16.21.254/24	172.16.22.254/24
Group_012	172.16.23.7/24		172.16.24.7/24	DHCP	172.16.23.254/24	172.16.24.254/24
Group_013	172.16.25.7/24		172.16.26.7/24	DHCP	172.16.25.254/24	172.16.26.254/24
Group_014	172.16.27.7/24		172.16.28.7/24	DHCP	172.16.27.254/24	172.16.28.254/24
Group_015	172.16.29.7/24		172.16.30.7/24	DHCP	172.16.29.254/24	172.16.30.254/24
Group_016	172.16.31.7/24		172.16.32.7/24	DHCP	172.16.31.254/24	172.16.32.254/24
Group_017	172.16.33.7/24		172.16.34.7/24	DHCP	172.16.33.254/24	172.16.34.254/24
Group_018	172.16.35.7/24		172.16.36.7/24	DHCP	172.16.35.254/24	172.16.36.254/24
Group_019	172.16.37.7/24		172.16.38.7/24	DHCP	172.16.37.254/24	172.16.38.254/24
Group_020	172.16.39.7/24		172.16.40.7/24	DHCP	172.16.39.254/24	172.16.40.254/24
Group_021	172.16.41.7/24		172.16.42.7/24	DHCP	172.16.41.254/24	172.16.42.254/24
Group_022	172.16.43.7/24		172.16.44.7/24	DHCP	172.16.43.254/24	172.16.44.254/24
Group_023	172.16.45.7/24		172.16.46.7/24	DHCP	172.16.45.254/24	172.16.46.254/24
Group_024	172.16.47.7/24		172.16.48.7/24	DHCP	172.16.47.254/24	172.16.48.254/24
Group_025	172.16.49.7/24		172.16.50.7/24	DHCP	172.16.49.254/24	172.16.50.254/24
Group_026	172.16.51.7/24		172.16.52.7/24	DHCP	172.16.51.254/24	172.16.52.254/24
Group_027	172.16.53.7/24		172.16.54.7/24	DHCP	172.16.53.254/24	172.16.54.254/24
Group_028	172.16.55.7/24		172.16.56.7/24	DHCP	172.16.55.254/24	172.16.56.254/24
Group_029	172.16.57.7/24		172.16.58.7/24	DHCP	172.16.57.254/24	172.16.58.254/24
Group_030	172.16.59.7/24		172.16.60.7/24	DHCP	172.16.59.254/24	172.16.60.254/24
Group_031	172.16.61.7/24		172.16.62.7/24	DHCP	172.16.61.254/24	172.16.62.254/24
Group_032	172.16.63.7/24		172.16.64.7/24	DHCP	172.16.63.254/24	172.16.64.254/24
Group_033	172.16.65.7/24		172.16.66.7/24	DHCP	172.16.65.254/24	172.16.66.254/24
Group_034	172.16.67.7/24		172.16.68.7/24	DHCP	172.16.67.254/24	172.16.68.254/24
Group_035	172.16.69.7/24		172.16.70.7/24	DHCP	172.16.69.254/24	172.16.70.254/24
Group_036	172.16.71.7/24		172.16.72.7/24	DHCP	172.16.71.254/24	172.16.72.254/24
Group_037	172.16.73.7/24		172.16.74.7/24	DHCP	172.16.73.254/24	172.16.74.254/24
Group_038	172.16.75.7/24		172.16.76.7/24	DHCP	172.16.75.254/24	172.16.76.254/24
Group_039	172.16.77.7/24		172.16.78.7/24	DHCP	172.16.77.254/24	172.16.78.254/24
Group_040	172.16.79.7/24		172.16.80.7/24	DHCP	172.16.79.254/24	172.16.80.254/24
Group_041	172.16.81.7/24		172.16.82.7/24	DHCP	172.16.81.254/24	172.16.82.254/24
Group_042	172.16.83.7/24		172.16.84.7/24	DHCP	172.16.83.254/24	172.16.84.254/24
Group_043	172.16.85.7/24		172.16.86.7/24	DHCP	172.16.85.254/24	172.16.86.254/24
Group_044	172.16.87.7/24		172.16.88.7/24	DHCP	172.16.87.254/24	172.16.88.254/24
Group_045	172.16.89.7/24		172.16.90.7/24	DHCP	172.16.89.254/24	172.16.90.254/24
Group_046	172.16.91.7/24		172.16.92.7/24	DHCP	172.16.91.254/24	172.16.92.254/24
Group_047	172.16.93.7/24		172.16.94.7/24	DHCP	172.16.93.254/24	172.16.94.254/24
Group_048	172.16.95.7/24		172.16.96.7/24	DHCP	172.16.95.254/24	172.16.96.254/24
Group_049	172.16.97.7/24		172.16.98.7/24	DHCP	172.16.97.254/24	172.16.98.254/24
Group_050	172.16.99.7/24		172.16.100.7/24 DHCP	172.16.99.254/24	172.16.100.254/24
Group_051	172.16.101.7/24	172.16.102.7/24 DHCP	172.16.101.254/24	172.16.102.254/24
Group_052	172.16.103.7/24	172.16.104.7/24 DHCP	172.16.103.254/24	172.16.104.254/24
Group_053	172.16.105.7/24	172.16.106.7/24 DHCP	172.16.105.254/24	172.16.106.254/24
Group_054	172.16.107.7/24	172.16.108.7/24 DHCP	172.16.107.254/24	172.16.108.254/24
Group_055	172.16.109.7/24	172.16.110.7/24 DHCP	172.16.109.254/24	172.16.110.254/24
Group_056	172.16.111.7/24	172.16.112.7/24 DHCP	172.16.111.254/24	172.16.112.254/24
Group_057	172.16.113.7/24	172.16.114.7/24 DHCP	172.16.113.254/24	172.16.114.254/24
Group_058	172.16.115.7/24	172.16.116.7/24 DHCP	172.16.115.254/24	172.16.116.254/24
Group_059	172.16.117.7/24	172.16.118.7/24 DHCP	172.16.117.254/24	172.16.118.254/24
Group_060	172.16.119.7/24	172.16.120.7/24 DHCP	172.16.119.254/24	172.16.120.254/24
Group_061	172.16.121.7/24	172.16.122.7/24 DHCP	172.16.121.254/24	172.16.122.254/24
Group_062	172.16.123.7/24	172.16.124.7/24 DHCP	172.16.123.254/24	172.16.124.254/24
Group_063	172.16.125.7/24	172.16.126.7/24 DHCP	172.16.125.254/24	172.16.126.254/24
Group_064	172.16.127.7/24	172.16.128.7/24 DHCP	172.16.127.254/24	172.16.128.254/24
Group_065	172.16.129.7/24	172.16.130.7/24 DHCP	172.16.129.254/24	172.16.130.254/24
Group_066	172.16.131.7/24	172.16.132.7/24 DHCP	172.16.131.254/24	172.16.132.254/24
Group_067	172.16.133.7/24	172.16.134.7/24 DHCP	172.16.133.254/24	172.16.134.254/24
Group_068	172.16.135.7/24	172.16.136.7/24 DHCP	172.16.135.254/24	172.16.136.254/24
Group_069	172.16.137.7/24	172.16.138.7/24 DHCP	172.16.137.254/24	172.16.138.254/24
Group_070	172.16.139.7/24	172.16.140.7/24 DHCP	172.16.139.254/24	172.16.140.254/24
Group_071	172.16.141.7/24	172.16.142.7/24 DHCP	172.16.141.254/24	172.16.142.254/24
Group_072	172.16.143.7/24	172.16.144.7/24 DHCP	172.16.143.254/24	172.16.144.254/24
Group_073	172.16.145.7/24	172.16.146.7/24 DHCP	172.16.145.254/24	172.16.146.254/24
Group_074	172.16.147.7/24	172.16.148.7/24 DHCP	172.16.147.254/24	172.16.148.254/24
Group_075	172.16.149.7/24	172.16.150.7/24 DHCP	172.16.149.254/24	172.16.150.254/24
Group_075	172.16.151.7/24	172.16.152.7/24 DHCP	172.16.151.254/24	172.16.152.254/24
Group_077	172.16.153.7/24	172.16.154.7/24 DHCP	172.16.153.254/24	172.16.154.254/24
Group_078	172.16.155.7/24	172.16.156.7/24 DHCP	172.16.155.254/24	172.16.156.254/24
Group_079	172.16.157.7/24	172.16.158.7/24 DHCP	172.16.157.254/24	172.16.158.254/24
Group_080	172.16.159.7/24	172.16.160.7/24 DHCP	172.16.159.254/24	172.16.160.254/24
Group_081	172.16.161.7/24	172.16.162.7/24 DHCP	172.16.161.254/24	172.16.162.254/24
Group_082	172.16.163.7/24	172.16.164.7/24 DHCP	172.16.163.254/24	172.16.164.254/24
Group_083	172.16.165.7/24	172.16.166.7/24 DHCP	172.16.165.254/24	172.16.166.254/24
Group_084	172.16.167.7/24	172.16.168.7/24 DHCP	172.16.167.254/24	172.16.168.254/24
Group_085	172.16.169.7/24	172.16.170.7/24 DHCP	172.16.169.254/24	172.16.170.254/24
Group_086	172.16.171.7/24	172.16.172.7/24 DHCP	172.16.171.254/24	172.16.172.254/24
Group_087	172.16.173.7/24	172.16.174.7/24 DHCP	172.16.173.254/24	172.16.174.254/24
</pre>


### Allocation C
<pre>
Allocated	Ubuntu	        Windows	        Em0	    Em1 (Private)	Em2 (DMZ)
-----------------------------------------------------------------------------------
Group_001	10.10.1.7/24	10.10.2.7/24	DHCP	10.10.1.254/24	10.10.2.254/24
Group_002	10.10.3.7/24	10.10.4.7/24	DHCP	10.10.3.254/24	10.10.4.254/24
Group_003	10.10.5.7/24	10.10.6.7/24	DHCP	10.10.5.254/24	10.10.6.254/24
Group_004	10.10.7.7/24	10.10.8.7/24	DHCP	10.10.7.254/24	10.10.8.254/24
Group_005	10.10.9.7/24	10.10.10.7/24	DHCP	10.10.9.254/24	10.10.10.254/24
Group_006	10.10.11.7/24	10.10.12.7/24	DHCP	10.10.11.254/24	10.10.12.254/24
Group_007	10.10.13.7/24	10.10.14.7/24	DHCP	10.10.13.254/24	10.10.14.254/24
Group_008	10.10.15.7/24	10.10.16.7/24	DHCP	10.10.15.254/24	10.10.16.254/24
Group_009	10.10.17.7/24	10.10.18.7/24	DHCP	10.10.17.254/24	10.10.18.254/24
Group_010	10.10.19.7/24	10.10.20.7/24	DHCP	10.10.19.254/24	10.10.20.254/24
Group_011	10.10.21.7/24	10.10.22.7/24	DHCP	10.10.21.254/24	10.10.22.254/24
Group_012	10.10.23.7/24	10.10.24.7/24	DHCP	10.10.23.254/24	10.10.24.254/24
Group_013	10.10.25.7/24	10.10.26.7/24	DHCP	10.10.25.254/24	10.10.26.254/24
Group_014	10.10.27.7/24	10.10.28.7/24	DHCP	10.10.27.254/24	10.10.28.254/24
Group_015	10.10.29.7/24	10.10.30.7/24	DHCP	10.10.29.254/24	10.10.30.254/24
Group_016	10.10.31.7/24	10.10.32.7/24	DHCP	10.10.31.254/24	10.10.32.254/24
Group_017	10.10.33.7/24	10.10.34.7/24	DHCP	10.10.33.254/24	10.10.34.254/24
Group_018	10.10.35.7/24	10.10.36.7/24	DHCP	10.10.35.254/24	10.10.36.254/24
Group_019	10.10.37.7/24	10.10.38.7/24	DHCP	10.10.37.254/24	10.10.38.254/24
Group_020	10.10.39.7/24	10.10.40.7/24	DHCP	10.10.39.254/24	10.10.40.254/24
Group_021	10.10.41.7/24	10.10.42.7/24	DHCP	10.10.41.254/24	10.10.42.254/24
Group_022	10.10.43.7/24	10.10.44.7/24	DHCP	10.10.43.254/24	10.10.44.254/24
Group_023	10.10.45.7/24	10.10.46.7/24	DHCP	10.10.45.254/24	10.10.46.254/24
Group_024	10.10.47.7/24	10.10.48.7/24	DHCP	10.10.47.254/24	10.10.48.254/24
Group_025	10.10.49.7/24	10.10.50.7/24	DHCP	10.10.49.254/24	10.10.50.254/24
Group_026	10.10.51.7/24	10.10.52.7/24	DHCP	10.10.51.254/24	10.10.52.254/24
Group_027	10.10.53.7/24	10.10.54.7/24	DHCP	10.10.53.254/24	10.10.54.254/24
Group_028	10.10.55.7/24	10.10.56.7/24	DHCP	10.10.55.254/24	10.10.56.254/24
Group_029	10.10.57.7/24	10.10.58.7/24	DHCP	10.10.57.254/24	10.10.58.254/24
Group_030	10.10.59.7/24	10.10.60.7/24	DHCP	10.10.59.254/24	10.10.60.254/24
Group_031	10.10.61.7/24	10.10.62.7/24	DHCP	10.10.61.254/24	10.10.62.254/24
Group_032	10.10.63.7/24	10.10.64.7/24	DHCP	10.10.63.254/24	10.10.64.254/24
Group_033	10.10.65.7/24	10.10.66.7/24	DHCP	10.10.65.254/24	10.10.66.254/24
Group_034	10.10.67.7/24	10.10.68.7/24	DHCP	10.10.67.254/24	10.10.68.254/24
Group_035	10.10.69.7/24	10.10.70.7/24	DHCP	10.10.69.254/24	10.10.70.254/24
Group_036	10.10.71.7/24	10.10.72.7/24	DHCP	10.10.71.254/24	10.10.72.254/24
Group_037	10.10.73.7/24	10.10.74.7/24	DHCP	10.10.73.254/24	10.10.74.254/24
Group_038	10.10.75.7/24	10.10.76.7/24	DHCP	10.10.75.254/24	10.10.76.254/24
Group_039	10.10.77.7/24	10.10.78.7/24	DHCP	10.10.77.254/24	10.10.78.254/24
Group_040	10.10.79.7/24	10.10.80.7/24	DHCP	10.10.79.254/24	10.10.80.254/24
Group_041	10.10.81.7/24	10.10.82.7/24	DHCP	10.10.81.254/24	10.10.82.254/24
Group_042	10.10.83.7/24	10.10.84.7/24	DHCP	10.10.83.254/24	10.10.84.254/24
Group_043	10.10.85.7/24	10.10.86.7/24	DHCP	10.10.85.254/24	10.10.86.254/24
Group_044	10.10.87.7/24	10.10.88.7/24	DHCP	10.10.87.254/24	10.10.88.254/24
Group_045	10.10.89.7/24	10.10.90.7/24	DHCP	10.10.89.254/24	10.10.90.254/24
Group_046	10.10.91.7/24	10.10.92.7/24	DHCP	10.10.91.254/24	10.10.92.254/24
Group_047	10.10.93.7/24	10.10.94.7/24	DHCP	10.10.93.254/24	10.10.94.254/24
Group_048	10.10.95.7/24	10.10.96.7/24	DHCP	10.10.95.254/24	10.10.96.254/24
Group_049	10.10.97.7/24	10.10.98.7/24	DHCP	10.10.97.254/24	10.10.98.254/24
Group_050	10.10.99.7/24	10.10.100.7/24 DHCP	    10.10.99.254/24	10.10.100.254/24
Group_051	10.10.101.7/24	10.10.102.7/24 DHCP	    10.10.101.254/24	10.10.102.254/24
Group_052	10.10.103.7/24	10.10.104.7/24 DHCP	    10.10.103.254/24	10.10.104.254/24
Group_053	10.10.105.7/24	10.10.106.7/24 DHCP	    10.10.105.254/24	10.10.106.254/24
Group_054	10.10.107.7/24	10.10.108.7/24 DHCP	    10.10.107.254/24	10.10.108.254/24
Group_055	10.10.109.7/24	10.10.110.7/24 DHCP	    10.10.109.254/24	10.10.110.254/24
Group_056	10.10.111.7/24	10.10.112.7/24 DHCP	    10.10.111.254/24	10.10.112.254/24
Group_057	10.10.113.7/24	10.10.114.7/24 DHCP	10.10.113.254/24	10.10.114.254/24
Group_058	10.10.115.7/24	10.10.116.7/24 DHCP	10.10.115.254/24	10.10.116.254/24
Group_059	10.10.117.7/24	10.10.118.7/24 DHCP	10.10.117.254/24	10.10.118.254/24
Group_060	10.10.119.7/24	10.10.120.7/24 DHCP	10.10.119.254/24	10.10.120.254/24
Group_061	10.10.121.7/24	10.10.122.7/24 DHCP	10.10.121.254/24	10.10.122.254/24
Group_062	10.10.123.7/24	10.10.124.7/24 DHCP	10.10.123.254/24	10.10.124.254/24
Group_063	10.10.125.7/24	10.10.126.7/24 DHCP	10.10.125.254/24	10.10.126.254/24
Group_064	10.10.127.7/24	10.10.128.7/24 DHCP	10.10.127.254/24	10.10.128.254/24
Group_065	10.10.129.7/24	10.10.130.7/24 DHCP	10.10.129.254/24	10.10.130.254/24
Group_066	10.10.131.7/24	10.10.132.7/24 DHCP	10.10.131.254/24	10.10.132.254/24
Group_067	10.10.133.7/24	10.10.134.7/24 DHCP	10.10.133.254/24	10.10.134.254/24
Group_068	10.10.135.7/24	10.10.136.7/24 DHCP	10.10.135.254/24	10.10.136.254/24
Group_069	10.10.137.7/24	10.10.138.7/24 DHCP	10.10.137.254/24	10.10.138.254/24
Group_070	10.10.139.7/24	10.10.140.7/24 DHCP	10.10.139.254/24	10.10.140.254/24
Group_071	10.10.141.7/24	10.10.142.7/24 DHCP	10.10.141.254/24	10.10.142.254/24
Group_072	10.10.143.7/24	10.10.144.7/24 DHCP	10.10.143.254/24	10.10.144.254/24
Group_073	10.10.145.7/24	10.10.146.7/24 DHCP	10.10.145.254/24	10.10.146.254/24
Group_074	10.10.147.7/24	10.10.148.7/24 DHCP	10.10.147.254/24	10.10.148.254/24
Group_075	10.10.149.7/24	10.10.150.7/24 DHCP	10.10.149.254/24	10.10.150.254/24
Group_075	10.10.151.7/24	10.10.152.7/24 DHCP	10.10.151.254/24	10.10.152.254/24
Group_077	10.10.153.7/24	10.10.154.7/24 DHCP	10.10.153.254/24	10.10.154.254/24
Group_078	10.10.155.7/24	10.10.156.7/24 DHCP	10.10.155.254/24	10.10.156.254/24
Group_079	10.10.157.7/24	10.10.158.7/24 DHCP	10.10.157.254/24	10.10.158.254/24
Group_080	10.10.159.7/24	10.10.160.7/24 DHCP	10.10.159.254/24	10.10.160.254/24
Group_081	10.10.161.7/24	10.10.162.7/24 DHCP	10.10.161.254/24	10.10.162.254/24
Group_082	10.10.163.7/24	10.10.164.7/24 DHCP	10.10.163.254/24	10.10.164.254/24
Group_083	10.10.165.7/24	10.10.166.7/24 DHCP	10.10.165.254/24	10.10.166.254/24
Group_084	10.10.167.7/24	10.10.168.7/24 DHCP	10.10.167.254/24	10.10.168.254/24
Group_085	10.10.169.7/24	10.10.170.7/24 DHCP	10.10.169.254/24	10.10.170.254/24
Group_086	10.10.171.7/24	10.10.172.7/24 DHCP	10.10.171.254/24	10.10.172.254/24
Group_087	10.10.173.7/24	10.10.174.7/24 DHCP	10.10.173.254/24	10.10.174.254/24
Group_088	10.10.175.7/24	10.10.176.7/24 DHCP	10.10.175.254/24	10.10.176.254/24

Group_089	10.10.210.7/24	10.10.211.7/24 DHCP	10.10.210.254/24	10.10.211.254/24
Group_090	10.10.181.7/24	10.10.182.7/24 DHCP	10.10.181.254/24	10.10.182.254/24
Group_091	10.10.179.7/24	10.10.180.7/24 DHCP	10.10.179.254/24	10.10.180.254/24

Group_092	10.10.183.7/24	10.10.184.7/24 DHCP	10.10.183.254/24	10.10.184.254/24
Group_093	10.10.185.7/24	10.10.186.7/24 DHCP	10.10.185.254/24	10.10.186.254/24
Group_094	10.10.187.7/24	10.10.188.7/24 DHCP	10.10.187.254/24	10.10.188.254/24
Group_095	10.10.189.7/24	10.10.190.7/24 DHCP	10.10.189.254/24	10.10.190.254/24
Group_096	10.10.191.7/24	10.10.192.7/24 DHCP	10.10.191.254/24	10.10.192.254/24
Group_097	10.10.193.7/24	10.10.194.7/24 DHCP	10.10.193.254/24	10.10.194.254/24
Group_098	10.10.195.7/24	10.10.196.7/24 DHCP	10.10.195.254/24	10.10.196.254/24
Group_099	10.10.197.7/24	10.10.198.7/24 DHCP	10.10.197.254/24	10.10.198.254/24
Group_100	10.10.199.7/24	10.10.200.7/24 DHCP	10.10.199.254/24	10.10.200.254/24
Group_101	10.10.201.7/24	10.10.202.7/24 DHCP	10.10.201.254/24	10.10.202.254/24
Group_102	10.10.203.7/24	10.10.204.7/24 DHCP	10.10.203.254/24	10.10.204.254/24
Group_103	10.10.205.7/24	10.10.206.7/24 DHCP	10.10.205.254/24	10.10.206.254/24
</pre>


