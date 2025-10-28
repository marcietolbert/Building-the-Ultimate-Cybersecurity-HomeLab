# Nessus Vulnerability Scanning
We have now reached Lab Five in the "Building the Ultimate Cybersecurity Homelab" series. At this point, if you’ve gone through the lab series sequentially, you are now ready to tackle vulnerability scanning, which is a way for both attackers and defenders to find security weaknesses in a system, network, or application, such as missing patches and misconfigurations. Vulnerability scanning helps organizations proactively strengthen their defenses, prioritize security risks, and maintain compliance with various regulations. Making it necessary for us as cybersecurity professionals to both know how vulnerability scanning works and how to perform a scan. First, let’s talk a little about the tool we will be using to conduct our scans for this lab, Nessus.

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

Click on Discovery and fill out the following:
- Host Discovery: Ping the remote host - On
- Test the local Nessus host - checked (allows Nessus to test the computer it’s installed on)
- Use fast network discovery- checked (ignores selected false positives that might appear)
- Ping Method: ARP - checked, TCP - checked, was aAICMP - checked
- Port Scanning: SYN -checked, TCP -checked

Click the Save button

On the My Scans page, you should see the Host Discovery Scan that we just configured. Click the play button next to the red X to launch the scan.

After the scan has completed, click the scan name to view the results.

The Hosts page displays the devices that the scan discovered. Under the "Vulnerabilities" tab, you can see what vulnerabilities it attempted to scan for. And if you look to the far right, you can see details about the scan and a vulnerabilities graph underneath.

## Vulnerability Scan
Let’s do a second scan. Click on "My Scans," then select "New Folder" and name it as desired. I’ll name mine -. Then click Create.

Click on the new folder you created in the left pane, then click the New Scan button. 

Click on Basic Network Scan under the Vulnerabilities section.

Fill out the following for our new scan settings:
Name: Vuln Scan
Description: This is my first time scanning for vulnerabilities 
Folder: —
Targets: 10.0.0.11
Under Schedule switch Enabled to an off state

Click on the Credentials Tab, then click SSH. 

For the authentication method, select password.
Enter msfadmin for both the username and password.

Then click the down arrow at the bottom of the page next to Save and click Launch. 

If you receive a pop-up about saving login information, click "Don’t Save."

Then click the — folder on the left side to access the scan.

Give the scan a few minutes to complete.

After the scan completes, click the scan’s name.

The first thing you see is a vulnerability rating based on severity level. Above this, you can see tabs for vulnerabilities and remediations. 

Click on the vulnerabilities tab.

You will see each vulnerability listed individually and can apply filters to narrow down the results. 

Try using a filter to narrow down the results to a severity level of critical.

Let’s drill into one of the vulnerabilities. Click on the Shellshock vulnerability.

The information returned about the vulnerability includes information such as the description, solution, links to additional information, and output.

To the right of the main pane, you can see information such as plugin details, vpr key drivers, risk and vulnerability information, and exploitable with.

Click on the vulnerabilities tab again and select the backdoor vulnerability. Look over the results provided.

If you click on the Remediations tab, it will provide a list of remediations, along with the vulnerabilities each remediation addresses.

Return to the Vulnerabilities tab and clear the filter. 

The value of using a vulnerability scanner lies not only in the tool's ability to identify assets and detect vulnerabilities. The value also comes in knowing what your assets are, what your Crown Jewels are, and remediating based on that assessment, which means that you may not always be acting on what’s most critical. Suppose you have a crown jewel with a high-severity vulnerability and an asset with a critical vulnerability, which asset should be remediated first? Based on the importance of the Crown Jewel to the organization and the impact of that asset being compromised, I would choose to￼ remediate the Crown Jewel first.￼

Let’s now look at how to create a report. Click on the report button at the top right.

On the Generate Report window, the first thing you see is the report format. You can choose between HTML, PDF, and CVS. You can then select the template you wish to use below. 

Let’s create a report in a PDF format using the Create List of Vulnerabilities by Host template and click on the Generate Report button.

Once the report opens, scroll through it to see how it’s formatted. 

As stated in the lab reports, these are great resources to present to management.

## Malware Scan
Lastly, let’s do a basic Malware Scan. Click on My Scans > New Scan and select Malware Scan. 

Use the following information:
Name: Malware Scan
Description: I am scanning for any malware on the Meta computer.
Target: 10.0.0.11

Click on the credentials tab and enter the following:
Authentication Method: password
Username: msfadmin
Password: msfadmin

Click Save.

Launch the malware scan by clicking the play button.

Once completed, click on the name of the scan to view the results.

Select the host IP address.

You should see one critical result listed. Select the result to view information. 
