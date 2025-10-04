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

## man and Shell Built-ins
First, power on the Kali Linux and Meta machines and sign in to both.

Open a terminal on the Kali Linux machine.

When dealing with any command, you might occasionally need help understanding the command's purpose and how it operates. To find answers, try using the Internet with specialized sites, such as Explain Shell, which can help you analyze commands and understand how they work. Alternatively, if you prefer to stay within the terminal, you can use the 'man' and 'help' commands.  

Linux categorizes its commands into four main types: external commands, shell built-ins, functions, and keywords. In this lab, we will focus only on external and shell built-in commands.

If we look at the ‘man’ command, it falls into the external command category. Why? That is because most commands are actual programs stored as binaries or scripts on disk, rather than being built into the shell. Typically in directories like /bin, /usr/bin, or /usr/local/bin. You can confirm that man is indeed a program by executing ￼the command " man which will output the absolute path of the executable file. When executed, the man command works by looking up formatted manual pages stored under /usr/share/man/.

The help command, on the other hand, functions as a shell built-in because the command is built directly into the shell (interpreter). You don’t need to search the file system, as the shell’s processes can execute the command code directly. Shell built-ins control various aspects of the shell, including navigation, environment, shell control, and utilities. The purpose of the help command is to display information solely about shell built-ins.

For commands that are not shell built-ins, there is a help variant known as double-dash help, which provides quick assistance on external programs. The program that the option applies to implements this command-line option.

Our next task in this lab will be to run both of these commands. First, let’s run ‘man tcpdump’ and examine the output.

**PHOTO**

Running the command above will output tcpdumps manual page. The page will display various sections, including a synopsis of the options relevant to the command, a description of the command, and a detailed options section where each option is defined.

Press *q* to quit.

Now, let’s try running the - - help option against the tcpdump command. tcpdump - -help

**PHOTO**

You will get a usage output for the various options tcpdump uses.

## tcpdump Lab
The first tool that we will be working with in this lab is tcpdump, so let's start there.

If you recall, tcpdump works by capturing network traffic from the network interface card. To see what interfaces are available for traffic capture run the following command: tcpdump -D

The system prints a list of available network interfaces from which tcpdump can capture packets.

**PHOTO**

For this lab, we will be working with eth0, which is the first interface listed in the output. Let’s clear the screen.

Now we will begin to capture network traffic from the eth0 interface by entering the following command: sudo tcpdump -i eth0

With this command, we instruct the shell to run tcpdump with elevated privileges to capture any network traffic that passes through the eth0 interface.

After we enter the kali user's password, tcpdump will begin capturing eth0 network traffic.

Let's start to generate some traffic by opening another terminal and pinging Google: ping google.com

As you can see, the ICMP Echo Request and Reply packets sent to and received from Google by the second terminal are being captured by tcpdump in the first terminal. 

Press Ctrl+C to stop the ping.

Let's examine one of the lines from the conversation that occurred between our endpoint and the Google server we contacted. The line contains several fields arranged from left to right: timestamp, source IP, destination, protocol used, message type, and flags.

Choose any line that shows an IMCP Echo Request as the protocol used (that would be our endpoint). Underneath that, on the following line, you should see the IMCP Echo Response protocol and the message type being used by the Google server to respond to our endpoint.

Clear the screen

Now that we have run a fairly basic scan, let’s try a capture that provides a more detailed output.

Run the following command:  sudo tcpdump -i eth0 -XA

The new command we are running keeps the exact requests from the first command and also prints the hex and ASCII representations of each packet, excluding the link-level header (Layer 2, according to the OSI model).

Now that we've defined the new capture we want to run, let's generate some traffic again: from the second terminal, ping the Meta machine: ping 10.0.0.11.

After letting the ping run for a few seconds, stop it using Ctrl+C

Let’s now look back at the first terminal for our tcpdump capture. Then scroll up to the start of the capture.

If we examine the first line of the first packet, we see that it presents the same type of information as the first capture. However, take a look at the second line of the packet. This line marks the start of the hex and ASCII information we requested with the -Xa option used at the end of the command we ran.


