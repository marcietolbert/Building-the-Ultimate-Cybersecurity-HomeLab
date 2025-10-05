### Nessus Vulnerability Scanning
We have now reached Lab Five in the "Building the Ultimate Cybersecurity Homelab" series. At this point, if you’ve gone through the lab series sequentially, you are now ready to tackle vulnerability scanning, which is a way for both attackers and defenders to find security weaknesses in a system, network, or application, such as missing patches and misconfigurations. ￼Vulnerability scanning helps organizations proactively strengthen their defenses, prioritize security risks, and maintain compliance with various regulations. Making it necessary for us as cybersecurity professionals to both know how vulnerability scanning works and how to perform a scan. First, let’s talk a little about the tool we will be using to conduct our scans for this lab, Nessus.

## What is Nessus
As stated above, we know that Nessus is one of many vulnerability scanners used to identify security weaknesses in systems, networks, and applications. But what specifically does Nessus do? If we break it down, the first thing Nessus does is scan systems for vulnerabilities, including known security issues, such as missing patches, misconfigurations, outdated software, and weak passwords. 

Secondly, Nessus uses a plugin database that contains the logic for detecting specific vulnerabilities (CVEs, misconfigurations, compliance violations). Next, Nessus can perform various types of scans, including credentialed and non-credentialed scans, as well as compliance scans. Credentialed scans are performed while logged in and, therefore, can conduct a more thorough check. Non-credentialed scans perform an external check without requiring a login. Compliance scans verify adherence to standards such as CIS benchmarks, PCI DSS, and HIPAA.

Lastly, Nessus produces detailed reports that rank the vulnerabilities found in a scan by severity (e.g., critical, high, medium, low), along with remediation recommendations.

To summarize, Nessus helps organizations identify and remediate security gaps before attackers can exploit them.


