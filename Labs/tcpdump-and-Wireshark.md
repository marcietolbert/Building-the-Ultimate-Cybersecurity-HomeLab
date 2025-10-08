# Sniffing Network Traffic with tcpdump and Wireshark
Welcome back to Lab Two in the **Building the Ultimate Cybersecurity Homelab** series! This write-up will discuss tcpdump and Wireshark, two network packet analysis tools that every cybersecurity professional should be familiar with.

First on our agenda is a review of tcpdump and Wireshark, highlighting their similarities, differences, and use cases.

## tcpdump vs Wireshark: A Head-to-Head Comparison 
Let's break down how tcpdump and Wireshark function in terms of the data they collect.

Three key elements are required for a network packet analyzer to analyze network packets: a network, a network stack, and network traffic. 

When two or more devices are connected together a LAN (Local Area Network) is formed, giving the devices the ability to exchange data and share resources. This means for example, that all of the connected devices in your home, through components such as a network interface card (enabling the device to physically join the LAN ), a switch, and/or wireless access points, are part of your local area network. It's important to note that the size of a LAN is generally limited to a specific area, such as a home, a single floor, or an office building.

However, the shared connection that links these devices together isn’t what allows them to "talk" to one another. For that, we need a network stack. A network stack is the implementation of networking protocols inside a device's operating system (and sometimes firmware/hardware) that allows a device to understand, send, and receive data over a network. We have models like the OSI and TCP/IP model that group these protocols into layers, which shows a theoretical and practical view (depending on which model you use) of how these layers operate.

We now have a network of devices on our LAN that can communicate with each other through a network stack. As these devices send and receive data over the network, they generate various types of traffic, including inbound, outbound, and broadcast traffic. It is this act the of data (data moving among multiple devices on the network) that creates network traffic.

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

Hexadecimal (hex) is a numbering system with a base of 16 that uses **0–9** and **A–F**. ASCII (**American Standard Code for Information Interchange**), on the other hand, is a character encoding standard that maps numbers to letters, digits, symbols, and control characters. The packet carries its payload—the content being delivered—in hex and ASCII values. Specifically, ￼hex is a representation of raw packet bytes while the ASCII is an interpretation of those bytes as characters (when printable).

In the first packet, our endpoint (10.0.0.11) is reaching out to or pinging (using ICMP) the Meta machine (10.0.0.1) to check if the machine is in an up state and able to converse by sending an Echo Request message. The hex and ASCII values we see indicate the payload (content delivered) to the Meta machine. Since the hexadecimal view of the payload is not human-readable, we need to examine the ASCII view, which displays a payload of 01234567.

Let’s now look for an Echo Reply message (response) from the Meta machine. 

The Echo Reply message below is the response from the Meta machine, echoing back the contents of the initial payload sent by our endpoint. This reply message confirms that the Meta machine is in an up state and ready to converse.

## Netcat
Now, before we jump into Wireshark, we are next tasked with exploring netcat, so let’s take a bit of a detour. Netcat, sometimes referred to as the Swiss Army knife of networking, serves as a versatile command-line utility that performs various network tasks, including creating and listening for connections, port scanning, data transfer, and more. For this lab, we will be using netcat to create and listen for connections.

As instructed, the first thing we will do is open three terminals. We already have two, so make sure those terminals have been cleared for a clean slate, and then open a third terminal. 

In the first terminal, we will use tcpdump to capture the traffic taking place over the network interface; however, we will capture traffic over the lo (loopback) interface instead of the eth0 interface.

Run the following command: sudo tcpdump -i lo -XA

Next, we need to create a netcat listener on the second terminal. To do that, we need to open a port for our listener to connect to. In our second terminal run the following command: nc -l -p 4444

This command instructs our shell to use netcat as a server, operating in listening mode (-l) and binding the listener to port 4444. The netcat listener will now be listening on port 4444.

Now run the following command in the third terminal: nc 127.0.0.1 4444

The command we just ran is telling the shell to use netcat to **open a TCP connection to port 4444 on the local machine (127.0.0.1)**.

We have now established an active connection between the second and third terminal.

Now, using either terminal, you can send messages back and forth between the two. Try it now by sending three to four messages from Terminal 2 to Terminal 3. Whatever you type into the second terminal should appear in the third terminal.

So, if we were to pretend our simulated lab were a real-world scenario￼, then Terminal Two would be our attack machine, where we would set up our listener and, using some payload, send it to our victim machine to compromise the machine and force it to connect back to the attacker’s listening machine.

Let’s jump back to our tcpdump capture to see what it logged.

Scroll through the packet captures to locate the first message you sent in the ASCII view. As you continue, you can follow the subsequent messages sent to Terminal 3.

Stop the capture: Ctrl+C

Clear the screen: clear

Now, let’s look at how to write tcpdump captures to a file. Run the following command. sudo tcpdump -i eth0 -w wakanda.pcap

This command instructs the shell to run a tcpdump capture with elevated privileges on the eth0 interface and to write the capture to a file named wakanda.pcap. 

To test this, pull up Terminal 2 or 3 and send a few more messages to the other terminal.

Then, terminate the connection to the other terminal using Ctrl+C

Close the third terminal, clear the screen on the second terminal, and then run the following command to ping the Meta machine: ping 10.0.0.11

Now, let’s run the following command to help generate more network traffic for our capture: ' ftp 10.0.0.11'.

Log in to the Meta machine with the mfsadmin credentials 

Close the terminal window, then stop the TCPdump capture currently running in the first terminal using Ctrl+C.

Now, if we run the 'ls' command, we can see that we have a wakanda.pcap file in our current working directory.

To read the capture, run the following command: sudo tcpdump -r wakanda.pcap. Using the -r option allows us to read the pcap file.

You can also run the -XA options against the file to view both the hex and ASCII representations.

Scroll through the capture to see what you can find related to logging into the Meta machine. 

Clear the screen.

## Wireshark
Now let’s open Wireshark.

Click the Kali logo in the upper left corner and search for Wireshark.

Let’s start capturing traffic on the eth0 interface just as we did in tcpdump by double-clicking the eth0 interface.

Start generating network traffic by opening the terminal and pinging the Meta machine four times using the following command: ping -c 4 10.0.0.11.

As the ping commences, Wireshark begins capturing the network traffic.

Minimize the terminal once the ping finishes.

What you are now seeing is the same information that was presented to us in tcpdump, just in a more aesthetically pleasing fashion. The column information is the same; from left to right, you have the timestamp, source IP, destination IP, protocol length, and info.

And if we examine the packets, you can clearly see the Echo request and reply packets. Since we selected a count of four ping packets, the Meta machine will send four reply responses.

The bottom right half of the screen displays the hex and ASCII information obtained when running our tcpdump capture with the -XA option. As you select each packet in the central pane, the hex and ASCII information will dynamically change to reflect the information for the selected packet. 

On the bottom left is the Packet Details pane, which provides a detailed breakdown of the selected packet's protocol. As you can see, this pane follows the structure of the OSI model. Choose a packet and click through each section in the packet details pane to see how the packet breaks down.

You can also right-click a packet and select Follow — Stream to view the packet details in another format.

You can now stop the capture by clicking the red stop button.

Lastly, let’s see how to read a PCAP file using Wireshark. Let’s use the wakanda.pcap file we saved from our tcpdump capture. Open the file using the terminal by running the command: wireshark wakanda.pcap

 Let’s use Wireshark’s display filter feature. If you recall, we used ftp to log in to the Meta machine. So let’s filter our traffic to display ftp only. In the search bar enter ftp. The central pane now only displays ftp traffic. 

Now, let’s try filtering for ICMP traffic by entering icmp into the search bar.

Search for ftp traffic again, then right-click on the first packet and select Follow > TCP Stream.

You can now see pertinent information￼, such as the tool used, credentials in clear text, and confirmation that the login was successful, which confirms that the credentials above are valid. 
