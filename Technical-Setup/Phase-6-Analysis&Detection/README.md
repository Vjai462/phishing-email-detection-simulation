## What We're Learning

In this phase, we will learn how to manually analyze an email and network traffic to find the telltale signs of a phishing attack. This is a fundamental skill for any cybersecurity professional. We'll use the data we already collected to find the evidence and understand how a real detection system would flag it as malicious.


## Tools Needed

- Your **Windows Server 2022 VM** (with the victim's email).
- Your **Kali Linux VM** (with Wireshark and the saved packet capture from Phase 5).
- A web browser.


## Step-by-Step Process

### **Step 1: Analyze the Email Headers**

An **email header** is like a digital postmark. It contains all the technical details about where an email came from, how it was routed, and what servers it passed through. A phishing email often has suspicious or mismatched information in its headers.

1. On your **Windows Server 2022 VM**, open the Thunderbird email client.
2. Open the phishing email you sent.
3. Go to the menu, click on **`View`**, then **`Headers`**, and select **`All`**. This will show you the full, raw email headers.
4. Look for these signs:
    - **Mismatching "From" and "Received" addresses:** The "From" field might say "Google Security," but the "Received" fields will show the email came from your `sber.local` server, which is a major red flag.
    - **IP Addresses:** Note the IP address in the `Received` header. This will be the IP of your GoPhish server, which is an Indicator of Compromise (IoC).
  
### **Step 2: Packet Analysis with Wireshark**

Now we will analyze the network traffic to find the username and password you submitted.

1. On your **Kali Linux VM**, open the Wireshark application.
2. Go to **`File` > `Open`** and select the packet capture file you saved from Phase 5.
3. In the filter bar at the top, type the following filter and press Enter:
`http.request.method == "POST"`
    - An **HTTP POST request** is what a web browser uses to send form data (like usernames and passwords) to a server. This filter helps us find the exact packet we are looking for.
4. You should see one or two packets appear. The "Info" column will say "POST /... HTTP/1.1".

### **Step 3: Find the Credentials**

1. Click on the POST request packet you found in the previous step.
2. In the bottom pane, right-click on the data and select **`Follow` > `HTTP Stream`**.
3. A new window will pop up showing the entire conversation between the victim's machine and your attacker VM. You will see the plain text of the password you entered (`Phished!`) right there in the data. This is the smoking gun!


## Success Checkpoints

- You were able to find the full headers of the phishing email.
- You used a Wireshark filter to find the specific `POST` request.
- You successfully found the submitted username and password in the Wireshark `HTTP Stream`.

## Key Concepts Learned

- **Email Header:** The invisible routing information attached to an email. Analyzing it reveals the true sender and path.
- **HTTP POST Request:** The standard way a browser sends information from a form (like a login page) to a server.
- **Indicator of Compromise (IoC):** A piece of evidence on a network or host that indicates a security breach has occurred. In our case, the mismatched headers and unencrypted password in Wireshark are IoCs.
- **Packet Analysis:** The process of examining network data to understand what's happening on the network.


## Phase Summary

*You have successfully completed a full manual analysis of your simulated phishing attack. You've learned how to find the digital evidence of the attack and understand how a system would flag it as malicious. This is a core skill in cybersecurity.*
