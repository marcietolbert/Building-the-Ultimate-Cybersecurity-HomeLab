# Sniffing Network Traffic with tcpdump and Wireshark
Welcome back to Lab Two in the **Building the Ultimate Cybersecurity Homelab** series! This write-up will discuss tcpdump and Wireshark, two network packet analysis tools that every cybersecurity professional should be familiar with.

First on our agenda is a review of tcpdump and Wireshark, highlighting their similarities, differences, and use cases.

## tcpdump vs Wireshark: A Head-to-Head Comparison 
Let's break down how tcpdump and Wireshark function in terms of the data they collect.

Three key elements are required for a network packet analyzer to analyze network packets (data): a network, a network stack, and network traffic.

For a network packet analyzer to function, there must be network traffic to analyze. So, how is network traffic generated? First, we need a network, and a typical example of this is a Local Area Network (LAN). 

When various types of connections, such as wired or wireless, are used to connect two or more devices, this forms a LAN, allowing said devices to exchange data and share resources. So, all connected devices in your home, which are connected through components such as a network interface card (enabling the device to join a LAN physically), a switch, and/or wireless access points, are part of your local area network. It's important to note that the size of a LAN is generally limited to a specific area, such as a home, a single floor, or an office building.

However, the shared connection that links them doesn't allow them to "talk" to one another. For that, we need a network stack. So just what is a network stack? A network stack is the implementation of networking protocols inside a device's operating system (and sometimes firmware/hardware) that allows a device to understand, send, and receive data over a network. We have models like the OSI and TCP/IP model that group these protocols into layers, which shows a theoretical and practical view (depending on which model you use) of how these layers operate.

Now, we have a network of devices on our LAN that can communicate with each other through a network stack. As these devices send and receive data over the network, they generate various types of traffic, including inbound, outbound, and broadcast traffic. Therefore, the exchange of data (the act of data moving among multiple devices on the network) is called network traffic.

Network packet analyzers such as tcpdump and Wireshark capture data units (data) from a device's network interface to inspect and decode packets across multiple network stack layers. With a network packet analyzer, you can capture and filter traffic, decode protocols, reconstruct sessions, troubleshoot network issues, and identify security problems, all while presenting the information in a human-readable format. We can now begin to see why tools like these are an invaluable resource.

Lastly, let's explore the differences between tcpdump and Wireshark. The main difference between the two is that tcpdump is a command-line-based tool while Wireshark is a GUI-based tool. Because of this, tcpdump is text only and therefore more lightweight than Wireshark, which is graphical and thus heavier on system resources. A good rule of thumb is to be knowledgeable in both, as you never know in the field which tool you may have to use.

## tcpdump Lab
First, power on the Kali Linux and Meta machines and sign in to both.

Open a terminal on the Kali Linux machine.

Now, when working with any command there might come a time when you will need some assistance in understanding what the command does and how it operates. In order to get answers to your question one could choose several ways to go about their research. One…you could to use the Internet ￼as a resource to leverage specialized sites such as explain shell to break commands and how they function. However, should you want to remain in the terminal there are you’d want to utilize: man and help. 

