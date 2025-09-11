## What We're Learning

In this phase, we'll set up **Wireshark**, which is a **network protocol analyzer**. Think of it as a security camera for your network. It captures and lets you look inside every single piece of data, called a **packet**, that travels across your network. For our project, we will use it to see exactly what happens when our victim clicks the phishing link, which will give us the hard evidence of the attack.


## Tools Needed

- Your **Kali Linux VM** .
- **Wireshark** (comes pre-installed on Kali).


## Step-by-Step Process

### **Step 1: Open Wireshark**

1. **Start your Kali Linux VM:** Power it on if it's not already running.
2. **Find Wireshark:** Click on the Kali Linux menu in the top-left corner. You can either find it under **"Tools"** or simply start typing "Wireshark" in the search box.
3. **Launch Wireshark:** Click on the Wireshark icon to open the program. It will ask for your password to run with special privileges, which it needs to "sniff" or capture network traffic.

### **Step 2: Choose the Correct Interface**

A **network interface** is the physical or virtual connection your computer uses to talk to a network. We need to tell Wireshark which one to watch.

1. When Wireshark opens, you will see a list of interfaces like `eth0`, `lo`, and others.
2. Look for the interface that has a lot of activity (a small graph next to it moving up and down). This is your active network connection. For our lab, it will likely be something like **`eth0`** or **`enp0s3`**.
3. **Double-click** on the correct interface to start capturing traffic.

### **Step 3: Capture Your First Packets**

1. Once you click on the interface, you'll see a flood of information. These are all the packets traveling on your network right now.
2. Now, let's generate some traffic ourselves. Open a new terminal on your Kali VM.
3. Type the following command and press Enter:
`ping -c 5 google.com`
    - **`ping`** is a simple command that sends a small packet to a website to see if it responds.
    - **`c 5`** tells it to only send 5 packets so we don't create too much noise.
4. As the `ping` command runs, go back to Wireshark. You will see new packets appear with the word "ICMP" in the **"Protocol"** column. This confirms you are successfully capturing traffic.


## Success Checkpoints

- You were able to successfully launch Wireshark on your Kali VM.
- You selected an active network interface and started the capture.
- The `ping` command successfully sent and received packets.
- You saw new packets with the **ICMP** protocol appearing in Wireshark.


## Key Concepts Learned

- **Wireshark:** A tool for capturing and analyzing network traffic.
- **Network Interface:** The connection point on your computer that sends and receives data.
- **Packet:** A small unit of data that travels over a network. Think of it as a tiny digital envelope with a piece of information, a sender's address, and a destination address.
- **Packet Sniffing:** The process of capturing and inspecting network packets.


## Phase Summary

In this phase, you've successfully set up Wireshark and learned how to "sniff" or capture network traffic. This is a powerful skill that will allow you to see and analyze the digital evidence of the phishing attack in our next phase.
