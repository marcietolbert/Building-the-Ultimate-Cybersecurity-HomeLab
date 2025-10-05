# Nessus Vulnerability Scanning
We have now reached Lab Five in the "Building the Ultimate Cybersecurity Homelab" series. At this point, if you’ve gone through the lab series sequentially, you are now ready to tackle vulnerability scanning, which is a way for both attackers and defenders to find security weaknesses in a system, network, or application, such as missing patches and misconfigurations. ￼Vulnerability scanning helps organizations proactively strengthen their defenses, prioritize security risks, and maintain compliance with various regulations. Making it necessary for us as cybersecurity professionals to both know how vulnerability scanning works and how to perform a scan. First, let’s talk a little about the tool we will be using to conduct our scans for this lab, Nessus.

## What is Nessus
As stated above, we know that Nessus is one of many vulnerability scanners used to identify security weaknesses in systems, networks, and applications. But what specifically does Nessus do? If we break it down, the first thing Nessus does is scan systems for vulnerabilities, including known security issues, such as missing patches, misconfigurations, outdated software, and weak passwords. 

Secondly, Nessus uses a plugin database that contains the logic for detecting specific vulnerabilities (CVEs, misconfigurations, compliance violations). Next, Nessus can perform various types of scans, including credentialed and non-credentialed scans, as well as compliance scans. Credentialed scans are performed while logged in and, therefore, can conduct a more thorough check. Non-credentialed scans perform an external check without requiring a login. Compliance scans verify adherence to standards such as CIS benchmarks, PCI DSS, and HIPAA.

Lastly, Nessus produces detailed reports that rank the vulnerabilities found in a scan by severity (e.g., critical, high, medium, low), along with remediation recommendations.

To summarize, Nessus helps organizations identify and remediate security gaps before attackers can exploit them.

## Discovery Scan

First, the lab instructs us to download Nessus and install its plugins on the Kali Linux virtual machine. I will not provide a walkthrough of the setup in this write-up; refer to the lab video here for the steps.

Next, we will be performing a discovery scan using Nessus. You should already be signed into the Kali Linux machine, as you needed to install Nessus onto it. Start and log in to the Meta and Ubuntu machines as well. 

So, what is a discovery scan? A discovery scan is a type of scan that focuses on identifying and locating network assets. These types of scans do not test the assets for vulnerabilities. A discovery scan can identify live hosts, find open ports and services, and collect system information. In essence, a discovery scan answers the question, “What’s on my network?”

After you have finished installing Nessus and downloading the plugins, you will need to wait for the plugins to compile, which may take a few minutes. You will then get a pop-up welcoming you to Nessus. Close the pop-up.

Let’s start our first discovery scan by clicking the blue 'New Scan' button.

On the Scan Templates page, click on Host Discovery under the Discovery section. *As stated before, this type of scan identifies the assets (devices) connected to our network.

To see what devices are part of our network, we need to perform a scan of the entire network range, which would be 10.0.0.0. 

Fill out the following for our new scan settings:
Name: History Discovery Scan
Description: This is my first time running Nessus
Folder: My Scans
Targets: 10.0.0.0
Under Schedule switch Enabled to an off state


