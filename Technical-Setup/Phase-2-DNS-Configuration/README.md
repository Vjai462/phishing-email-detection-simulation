## What We're Learning

In this phase, we'll learn about **DNS**, which stands for **Domain Name System**. Think of DNS as the internet's phone book. When you type `www.google.com` into your browser, DNS is the system that translates that easy-to-remember name into a difficult-to-remember IP address (like `142.250.191.46`). Without DNS, you'd have to remember the IP address for every website you want to visit.

For our project, we need to set up our own mini "phone book" so our virtual machines can find our mail server by its name (`sber.local`) instead of just its IP address (`192.168.1.10`). This will make our phishing attack simulations much more realistic. We will use our **pfSense VM** to act as our DNS server.


## Tools Needed

- Your **pfSense VM** (already set up).
- Your **Windows Server 2022 VM** (to check that DNS is working).
- A web browser to access the pfSense web interface.


## Step-by-Step Process

### **Step 1: Access the pfSense Web Interface**

1. **Start your pfSense VM:** Power on your pfSense virtual machine in VirtualBox.
2. **Find its IP Address:** Once it boots up, you'll see a console screen with two or more IP addresses. Look for the one next to **LAN**. This is the IP address of your pfSense box on your internal network. For example, it might be `192.168.1.1`.
3. **Log in:** On your host computer (your main PC), open a web browser and type the **LAN IP address** into the address bar.
4. You'll be prompted for a username and password. The defaults are usually **`admin`** and **`pfsense`**.

### **Step 2: Configure a DNS Host Override**

A **host override** is a way of telling our local network, "Hey, when anyone asks for this specific domain name, send them to this specific IP address instead of checking with a public DNS server." This is exactly what we need to make our `sber.local` domain work inside our lab.

1. **Navigate to the DNS Resolver settings:** In the pfSense web interface, go to **Services > DNS Resolver > Host Overrides**.
2. **Add a new override:** Click the **`+Add`** button.
3. Fill out the details:
    - **Host:** Type `sber`
    - **Domain:** Type `local`
    - **IP Address:** This needs to be the IP address of your **Windows Server 2022 VM** where hMailServer is running. You can find this by opening the command prompt (`cmd`) on your Windows Server VM and typing `ipconfig`. Find the IP address listed under your network adapter.
4. **Save the override:** Click **`Save`** at the bottom. A green banner should appear saying "The changes have been applied successfully."

### **Step 3: Configure the Windows Server to Use pfSense as its DNS Server**

For our Windows Server VM to use our new "phone book," we need to tell it to look at pfSense for DNS information.

1. On your **Windows Server 2022 VM**, open the **Control Panel**.
2. Go to **Network and Sharing Center > Change adapter settings**.
3. Right-click on your network connection and select **Properties**.
4. Find **"Internet Protocol Version 4 (TCP/IPv4)"** in the list and click **Properties**.
5. Select **"Use the following DNS server addresses"**.
6. In the **Preferred DNS server** field, enter the **LAN IP address of your pfSense VM** (e.g., `192.168.1.1`).
7. Click **OK** and close the windows.

### **Step 4: Test DNS Resolution**

Now, let's make sure it worked!

1. On your **Windows Server 2022 VM**, open the **Command Prompt** (`cmd`).
2. Type the following command and press Enter: `nslookup sber.local`
    - **`nslookup`** is a command used to "look up" a domain name and find its IP address.
3. **Check the output:** The command should return the IP address of your Windows Server 2022 VM. If it does, you have successfully configured DNS!


## Success Checkpoints

- After Step 2, you should see the `sber.local` host override listed in the pfSense web interface.
- After Step 3, the network settings on your Windows Server VM should show the pfSense IP as the DNS server.
- After Step 4, the `nslookup` command on your Windows Server VM should successfully show the IP address for `sber.local`.


## Key Concepts Learned

- **DNS (Domain Name System):** The system that translates human-readable domain names into machine-readable IP addresses.
- **pfSense:** A powerful open-source firewall and router that we're also using as our local DNS server.
- **Host Override:** A specific DNS setting that forces a domain name to point to a particular IP address, overriding public DNS settings. This is perfect for our isolated lab environment.
- **`nslookup`:** A command-line tool for troubleshooting DNS issues by looking up domain names.


## Phase Summary

In this phase, we've set up a critical part of our lab network: **DNS**. We've configured our pfSense firewall to act as a local DNS server and created a **host override** so that our virtual machines now know where to find `sber.local`. This makes our lab environment more realistic and prepares us for the next steps.
